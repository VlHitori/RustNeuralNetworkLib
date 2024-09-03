# Neural Network Library Documentation

This library provides a simple implementation of a neural network with fully connected layers. The library includes the following components:

- `Network`: The main structure representing the neural network.
- `Layer`: Represents a layer in the neural network.
- `Neuron`: Represents a single neuron in a layer.
- `LayerTopology`: A simple struct for defining the number of neurons in each layer.

## Network

### Overview
The `Network` struct represents a neural network consisting of multiple layers. It supports creating networks with random weights, initializing networks from predefined weights, propagating inputs through the network, and retrieving the weights of the network.

### Methods

- **`new(layers: Vec<Layer>) -> Network`**  
  Creates a new `Network` from the provided layers.
  ```rust
  let layers = vec![Layer::random(&mut rng, 3, 4), Layer::random(&mut rng, 4, 2)];
  let network = Network::new(layers);
-  **`random(rng: &mut dyn RngCore, layers: &[LayerTopology]) -> Network`**

    Creates a new `Network` with random weights. The number of neurons in each layer is defined by LayerTopology.

    ```rust
    let layers = [LayerTopology { neurons: 3 }, LayerTopology { neurons: 4 }, LayerTopology { neurons: 2 }];
    let network = Network::random(&mut rng, &layers);
-  **`from_weights(layers: &[LayerTopology], weights: impl IntoIterator<Item = f32>) -> Network`**

    Creates a new `Network` from the provided weights. The number of neurons in each layer is defined by `LayerTopology`, and the weights are provided as an iterator.

    ```rust
    let layers = [LayerTopology { neurons: 3 }, LayerTopology { neurons: 4 }, LayerTopology { neurons: 2 }];
    let weights = vec![0.1, 0.2, 0.3, ...];
    let network = Network::from_weights(&layers, weights);
-  **`propagate(&self, inputs: Vec<f32>) -> Vec<f32>`**

    Propagates the input values through the network and returns the output.

    ```rust
    let inputs = vec![1.0, 0.5, -1.5];
    let outputs = network.propagate(inputs);
-  **`weights(&self) -> impl Iterator<Item = f32> + '_`**

    Returns an iterator over the weights of the network.

    ```rust
    for weight in network.weights() {
        println!("{}", weight);
    }

## Layer
### Overview

The `Layer` struct represents a layer in the neural network, which consists of multiple neurons. It supports creating layers with random weights, initializing layers from predefined weights, and propagating inputs through the layer.
### Methods

-  **`new(neurons: Vec<Neuron>) -> Layer`**

    Creates a new `Layer` from the provided neurons.

    ```rust
    let neurons = vec![Neuron::random(&mut rng, 3), Neuron::random(&mut rng, 3)];
    let layer = Layer::new(neurons);
-  **`random(rng: &mut dyn RngCore, input_size: usize, output_size: usize) -> Layer`**

    Creates a `Layer` with random weights for the specified input and output sizes.

    ```rust
    let layer = Layer::random(&mut rng, 3, 4);
-  **`from_weights(input_size: usize, output_size: usize, weights: &mut dyn Iterator<Item = f32>) -> Layer`**

    Creates a new `Layer` from the provided weights.

    ```rust
    let weights = vec![0.1, 0.2, 0.3, ...];
    let layer = Layer::from_weights(3, 4, &mut weights.into_iter());
-  **`propagate(&self, inputs: Vec<f32>) -> Vec<f32>`**

    Propagates the input values through the layer and returns the output.

    ```rust
    let inputs = vec![1.0, 0.5, -1.5];
    let outputs = layer.propagate(inputs);

## Neuron
### Overview

The `Neuron` struct represents a single neuron in a layer. Each neuron has a bias and a set of weights corresponding to its input connections.
### Methods

-  **`new(bias: f32, weights: Vec<f32>) -> Neuron`**
    
    Creates a new `Neuron` with the given bias and weights.

    ```rust
    let neuron = Neuron::new(0.5, vec![0.1, 0.2, 0.3]);

-  **`random(rng: &mut dyn RngCore, input_size: usize) -> Neuron`**
    
    Creates a `Neuron` with random bias and weights.

    ```rust
    let neuron = Neuron::random(&mut rng, 3);

-  **`from_weights(input_size: usize, weights: &mut dyn Iterator<Item = f32>) -> Neuron`**

    Creates a new `Neuron` from the provided weights.

    ```rust
    let weights = vec![0.5, 0.1, 0.2, 0.3];
    let neuron = Neuron::from_weights(3, &mut weights.into_iter());

- **`propagate(&self, inputs: &[f32]) -> f32`**

    Propagates the input values through the neuron and returns the output.

    ```rust
    let inputs = vec![1.0, 0.5, -1.5];
    let output = neuron.propagate(&inputs);

## LayerTopology
### Overview

The `LayerTopology` struct is used to define the number of neurons in a layer. It is primarily used when creating a new `Network` with random weights.
### Fields

-  **`neurons: usize`**
    The number of neurons in the layer.

    ```rust
    let topology = LayerTopology { neurons: 3 };    