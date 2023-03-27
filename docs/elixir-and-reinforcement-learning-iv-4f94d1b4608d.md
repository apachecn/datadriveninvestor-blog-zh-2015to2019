# 灵丹妙药和强化学习——四

> 原文：<https://medium.datadriveninvestor.com/elixir-and-reinforcement-learning-iv-4f94d1b4608d?source=collection_archive---------7----------------------->

![](img/20a979b260c499ebee72ab9b3592beaf.png)

Connections

你想重新获得什么吗？？第三集。

## 神经网络

最后…..神经网络。

在这个冒险计划的第四集中，我们将只用灵药来创建汽车的神经网络。我研究了两种建立神经网络的方法。我对使用矩阵还是使用代理和链式过程持怀疑态度。

[](https://www.datadriveninvestor.com/2019/01/23/deep-learning-explained-in-7-steps/) [## 深度学习用 7 个步骤解释-更新|数据驱动的投资者

### 在深度学习的帮助下，自动驾驶汽车、Alexa、医学成像-小工具正在我们周围变得超级智能…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/23/deep-learning-explained-in-7-steps/) 

## 矩阵或代理

我在昆汀·托马斯的博客上读到了一篇有趣的文章，他在博客中使用了矩阵和数字库。但当我在 ElixirDaze 2016 上观看[卡门·布莱克](https://medium.com/u/5407589a1069?source=post_page-----4f94d1b4608d--------------------------------)的 [**演讲**](https://www.youtube.com/watch?time_continue=3&v=YE0h9DURSOo) 时，它引起了我的注意，展示了他如何使用 Erlang 过程创建他的神经网络。参加完这个讲座后，我决定将同样的想法用于我们的自动驾驶汽车。你可能会注意到，我的神经网络的基础几乎与卡门·布莱克创建的一样，作为预测行动的方法，几乎没有什么变化，神经元之间的权重现在是随机的，还有一些更小的变化。我在这里留下我对他的感谢。

## 开始…

在这里，我不会进入神经网络如何工作的理论细节，因为在专业网站上有大量的材料可以阅读。让我们创建一个新的目录来写神经网络代码:`lib/neural_network`。

我将创建的第一个文件叫做`network.ex.`这个文件我将用来定义神经网络，创建层，在层内创建神经元，并在它们之间建立连接。所有的预测和训练部分也将在这里。网络将具有数据结构来维护神经网络的状态，例如:pid、输入层、隐藏层和输出层。

```
# lib/neural_network/network.exdefmodule AutonomousCar.NeuralNetwork.Network do
  alias AutonomousCar.NeuralNetwork.{Layer, Network, Neuron}
  alias AutonomousCar.Math.Activation defstruct pid: nil, input_layer: nil, hidden_layers: [], output_layer: nil def start_link(layer_sizes \\ []) do
    {:ok, pid} = Agent.start_link(fn -> %Network{} end) layers =
      map_layers(
        input_neurons(layer_sizes),
        hidden_neurons(layer_sizes),
        output_neurons(layer_sizes)
      ) pid |> update_layers(layers)
    pid |> connect_layers
    {:ok, pid}
  end def get(pid), do: Agent.get(pid, &(&1)) def update_layers(pid, layers) do
    layers = Map.merge(layers, %{pid: pid})
    Agent.update(pid, &Map.merge(&1, layers))
  end def predict(network, input_values) do
    network.input_layer
    |> Layer.activate(:relu, input_values) Enum.each(network.hidden_layers, fn hidden_layer ->
      hidden_layer
      |> Layer.activate(:relu)
    end) network.output_layer
    |> Layer.activate(:sigmoid) prob_actions =
      network.output_layer
      |> Layer.get()
      |> Layer.neurons_output()
      |> Activation.calculate_output(:softmax) action =
      prob_actions
      |> Enum.find_index(fn value -> Enum.max(prob_actions) == value          end)
  end defp input_neurons(layer_sizes) do
    size = layer_sizes |> List.first()
    {:ok, pid} = Layer.start_link(%{neuron_size: size})
    pid
  end defp hidden_neurons(layer_sizes) do
    layer_sizes
    |> hidden_layer_slice
    |> Enum.map(fn size ->
      {:ok, pid} = Layer.start_link(%{neuron_size: size})
      pid
    end)
  end defp output_neurons(layer_sizes) do
    size = layer_sizes |> List.last()
    {:ok, pid} = Layer.start_link(%{neuron_size: size})
    pid
  end defp hidden_layer_slice(layer_sizes) do
    layer_sizes
    |> Enum.slice(1..(length(layer_sizes) - 2))
  end defp connect_layers(pid) do
    layers =
      pid
      |> Network.get()
      |> flatten_layers layers
    |> Stream.with_index()
    |> Enum.each(fn tuple ->
      {layer, index} = tuple
      next_index = index + 1 if Enum.at(layers, next_index) do
      Layer.connect(layer, Enum.at(layers, next_index))
    end
  end)
end defp flatten_layers(network) do
    [network.input_layer] ++ network.hidden_layers ++   [network.output_layer]
  end defp map_layers(input_layer, hidden_layers, output_layer) do
    %{
      input_layer: input_layer,
      output_layer: output_layer,
      hidden_layers: hidden_layers
    }
  end
end
```

注意，我们有一个`predict/2`方法，它将接收来自汽车传感器的输入数据和汽车相对于目标的方向，并将返回一个动作。而神经网络有 3 个动作输出:向右移动汽车 20 度，向左移动汽车 20 度，或者保持相同的角度。今天我们将不训练神经网络，这将是下一集的内容。

对于`predict`，我们将需要创建新的模块，如`Layer`、`Neuron`和`Connection`。并且还创建了激活功能`[ReLU](https://towardsdatascience.com/activation-functions-neural-networks-1cbd9f8d91d6)``[Sigmoid](https://towardsdatascience.com/activation-functions-neural-networks-1cbd9f8d91d6)``[Softmax](https://towardsdatascience.com/activation-functions-neural-networks-1cbd9f8d91d6)`。然后我们需要创建一个新文件:

```
# lib/math/activation.exdefmodule AutonomousCar.Math.Activation do def calculate_output(input, :softmax), do: softmax(input)
  def calculate_output(input, :sigmoid), do: sigmoid(input)
  def calculate_output(input, :relu), do: relu(input) defp softmax([input]), do: softmax(input)
  defp softmax(input) do
    max_input = Enum.max(input)
    x = Enum.map(input, fn(y) -> y-max_input end)
    sum = listsum(x)
    Enum.map(x, fn(y) -> :math.exp(y)/sum end)
  end defp listsum([]), do: 0
  defp listsum([x|xs]), do: :math.exp(x) + listsum(xs) defp sigmoid(input), do: 1 / (1 + :math.exp(-input)) defp relu(input) when input <= 0, do: 0
  defp relu(input) when input > 0, do: input
end
```

## 层模块

```
# lib/neural_network/layer.exdefmodule AutonomousCar.NeuralNetwork.Layer do alias AutonomousCar.NeuralNetwork.{Layer, Neuron} defstruct pid: nil, neurons: [] def start_link(layer_fields \\ %{}) do
    {:ok, pid} = Agent.start_link(fn -> %Layer{} end)
    neurons = create_neurons(Map.get(layer_fields, :neuron_size))
    pid |> update(%{pid: pid, neurons: neurons}) {:ok, pid}
  end def get(pid), do: Agent.get(pid, & &1) def update(pid, fields) do
    Agent.update(pid, &Map.merge(&1, fields))
  end defp create_neurons(nil), do: []
  defp create_neurons(size) when size < 1, do: []
  defp create_neurons(size) when size > 0 do
    Enum.into(1..size, [], fn _ ->
      {:ok, pid} = Neuron.start_link()
      pid
    end)
  end def add_neurons(layer_pid, neurons) do
    layer_pid |> update(%{neurons: get(layer_pid).neurons ++ neurons})
  end def connect(input_layer_pid, output_layer_pid) do
    input_layer = get(input_layer_pid) unless contains_bias?(input_layer) do
      {:ok, pid} = Neuron.start_link(%{bias?: true})
      input_layer_pid |> add_neurons([pid])
    end for source_neuron <- get(input_layer_pid).neurons,
        target_neuron <- get(output_layer_pid).neurons do
      Neuron.connect(source_neuron, target_neuron)
    end
  end defp contains_bias?(layer) do
    Enum.any?(layer.neurons, &Neuron.get(&1).bias?)
  end def activate(layer_pid, activation_type, values \\ nil) do
    layer = get(layer_pid)
    values = List.wrap(values) layer.neurons
    |> Stream.with_index()
    |> Enum.each(fn tuple ->
      {neuron, index} = tuple
      neuron |> Neuron.activate(activation_type, Enum.at(values, index))
    end)
    layer_pid
  end def neurons_output(layer) do
    layer.neurons
    |> Enum.map(&(Neuron.get(&1).output))
  end
end
```

## 神经元模块

```
# lib/neural_network/neuron.exdefmodule AutonomousCar.NeuralNetwork.Neuron do
  alias AutonomousCar.NeuralNetwork.{Connection, Neuron}
  alias AutonomousCar.Math.Activation defstruct pid: nil, input: 0, output: 0, incoming: [], outgoing: [], bias?: false, delta: 0 def start_link(neuron_fields \\ %{}) do
    {:ok, pid} = Agent.start_link(fn -> %Neuron{} end)
    update(pid, Map.merge(neuron_fields, %{pid: pid})) {:ok, pid}
  end def update(pid, neuron_fields) do
    Agent.update(pid, &Map.merge(&1, neuron_fields))
  end def get(pid), do: Agent.get(pid, & &1) def connect(source_neuron_pid, target_neuron_pid) do
    {:ok, connection_pid} = Connection.connection_for(source_neuron_pid, target_neuron_pid) source_neuron_pid
    |> update(%{outgoing: get(source_neuron_pid).outgoing ++ [connection_pid]}) target_neuron_pid
    |> update(%{incoming: get(target_neuron_pid).incoming ++ [connection_pid]})
  end def activate(neuron_pid, activation_type, value \\ nil) do
    neuron = get(neuron_pid) fields =
      if neuron.bias? do
        %{output: 1}
      else
        input = value || Enum.reduce(neuron.incoming, 0, summation())
        %{input: input, output: Activation.calculate_output(input, activation_type)}
      end neuron_pid |> update(fields)
  end defp summation do
    fn connection_pid, sum ->
      connection = Connection.get(connection_pid)
      sum + get(connection.source_pid).output * connection.weight
    end
  end
end
```

## 连接模块

```
# lib/neural_network/connection.exdefmodule AutonomousCar.NeuralNetwork.Connection do alias AutonomousCar.NeuralNetwork.Connection defstruct pid: nil, source_pid: nil, target_pid: nil, weight: 0.4 def start_link(connection_fields \\ %{}) do
    {:ok, pid} = Agent.start_link(fn -> %Connection{} end)
    update(pid, Map.merge(connection_fields, %{pid: pid, weight: :rand.uniform_real})) {:ok, pid}
  end def get(pid), do: Agent.get(pid, & &1) def update(pid, fields) do
    Agent.update(pid, fn connection -> Map.merge(connection, fields) end)
    Agent.update(pid, &Map.merge(&1, fields))
  end def connection_for(source_pid, target_pid) do
    {:ok, pid} = start_link()
    pid |> update(%{source_pid: source_pid, target_pid: target_pid}) {:ok, pid}
  end
end
```

## 让我们使用神经网络

随着网络代码的创建，让我们做一些改变，让我们的汽车开始使用网络，没有更多的键盘命令。

还记得我们的`lib/scenes/environment.ex`文件吗，我们从哪里开始赛车，环境等等？我们现在需要调用它内部的神经网络。

```
# lib/scenes/environment.exdefmodule AutonomousCar.Scene.Environment do
  use Scenic.Scene require Logger alias Scenic.Graph
  alias Scenic.ViewPort alias AutonomousCar.Math.Vector2
  alias AutonomousCar.Objects.Car **alias AutonomousCar.NeuralNetwork.Network** import Scenic.Primitives def init(_arg, opts) do

  ...(more)...
```

在`init/2`方法中，我们存储`state`，我们需要添加神经网络 **pid** ，汽车的最后位置坐标和传感器信号。而且我们不能忘记启动神经网络`Network.start_link/1`。为了跟上我们的灵感来源，这是 Udemy 在第 1 集评论的课程，我将用 5 个输入、30 个隐藏层神经元和 3 个输出神经元初始化网络。

```
# lib/scenes/environment.exdef init(_arg, opts) do 

  ... **# start neural network
  {:ok, neural_network_pid} = Network.start_link([5, 30, 3])** state = %{
    viewport: viewport,
    viewport_width: viewport_width,
    viewport_height: viewport_height,
    graph: graph,
    frame_count: 0,
    **neural_network_pid: neural_network_pid,**
    objects: %{
      car: %{
        dimension: %{ width: 20, height: 10},
        coords: {pos_x, pos_y},
        **last_coords: {pos_x, pos_y},**
        velocity: {1, 0},
        angle: 0,
        **signal: %{
          left: 0,
          center: 0,
          right: 0
        }**,
        sensor: %{
          left: {0, 0},
          center: {0, 0},
          right: {0, 0}
        }
      },
      goal: %{coords: {20,20}}
    }
  }

  ...
```

我们还需要修改`handle_info/2`方法来捕获当前的汽车数据，最新的坐标，将其发送到神经网络并根据目标定位汽车。

```
# lib/scenes/environment.ex...def handle_info(:frame, %{frame_count: frame_count} = state) do
  **# Current car position
  {car_x, car_y} = state.objects.car.coords** **# Last car position
  {car_last_x, car_last_y} = state.objects.car.last_coords** **# Current goal position
  {goal_x, goal_y} = state.objects.goal.coords** **# Vector1 - Current position minus previous position
  vector1 = Scenic.Math.Vector2.sub({car_x, car_y}, {car_last_x, car_last_y})** **# Vector2 - Current position goal minus previous position car
  vector2 = Scenic.Math.Vector2.sub({goal_x, goal_y}, {car_last_x, car_last_y})** **# Normalized vector1
  vector1_normalized = Scenic.Math.Vector2.normalize(vector1)** **# Normalized vector2
  vector2_normalized = Scenic.Math.Vector2.normalize(vector2)** **# Orientation
  orientation = Scenic.Math.Vector2.dot(vector1_normalized, vector2_normalized)** **# Radius Orientation
  orientation_rad = Math.acos(orientation)** **# Grad orientation
  orientation_grad = (180 / :math.pi) * orientation_rad** **# Signals
  signal_sensor_1 = 0
  signal_sensor_2 = 0
  signal_sensor_3 = 0** **# Deep Learning
  action =
    state.neural_network_pid
    |> Network.get()
    |> Network.predict([0, 0, 0, orientation, -orientation])** **state =
    state
    |> Car.update_rotation(action)** new_state =
    if rem(frame_count, 4) == 0 do
      state |> Car.move
    else
      state
    end graph =
    state.graph
    |> draw_objects(state.objects) {:noreply, new_state, push: graph}
end ... 
```

可以删除`handle_input/3`。

```
# lib/scenes/environment.ex...## Deleted**def handle_input({:key, {"left", :press, _}}, _context, state) do
  {:noreply, Car.update_rotation(state, 1)}
end****def handle_input({:key, {"right", :press, _}}, _context, state) do
  {:noreply, Car.update_rotation(state, 2)}
end****def handle_input(_input, _context, state), do: {:noreply, state}** ... 
```

## 准备好了…

现在这辆车已经有一个神经网络与之相连。但是，如果没有训练，你可以验证神经网络没有正确响应，导致汽车在圆周上移动。在下一集我们将看到如何训练她找到目标。在那之前。

## [https://github . com/marceloreichert/PWT-autonomous-car-medium](https://github.com/marceloreichert/pwt-autonomous-car-medium)