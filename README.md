## Abstract
*In traditional Federated Learning (FL), an aggregator server collects and coordinates updates
from client machines, resulting in a potential bottleneck in scalability and a single point of
failure. This project aims to evaluate the feasibility of Decentralized Federated Learning (DFL)
to utilize peer-to-peer (p2p) communication among clients to provide both high-performance and
resilient system architecture. Using a modified version of the flower framework to implement
gRPC protocol, this project allows client updates to flow directly to other clients without an
intermediary aggregator server. Results of experiments conducted with the MNIST dataset show
that our DFL architecture is capable of achieving model convergence, yielding an increase in
accuracy from 14% to 33% during three rounds of training while decreasing reliance on a
central aggregator server.*

## TABLE OF CONTENT
- 1. Introduction
- 2. Literature Review
- 3. Problem Statement & Objectives
- 4. Functional and Non-Functional Requirements
- 5. System Architecture and Design
- 6. Methodology and Implementation Details
- 7. Experiments and Result Analysis
- 8. Challenges and Discussions
- 9. Conclusion & Future Work
References

## LIST OF FIGURES
- Figure 1. Steps for Peer-to-peer FL Training
- Figure 2. Centralized Federated Learning Architecture
- Figure 3. High-Level Decentralized Federated Learning Design
- Figure 4. DFL Diagram
- Figure 5. FL Components in the System Diagram
- Figure 6. Data Flow Diagram for Decentralized Learning
- Figure 7. Flower Federated Learning Architecture
- Figure 8. Centralized Model Results
- Figure 9. Decentralized P2P Results
- Figure 10. Decentralized Workflow
- Figure 11. Training Logs of Decentralized FL System

## i.Introduction
Federated Learning is a method of collaborative machine learning where multiple clients can collectively
train a machine learning model without the need for a central repository of their data. Data is processed
by the clients themselves, i.e., the devices owned by the users, which include mobile phones, laptops, and
IoT nodes. Once the client completes training a portion of the model based on its local data, it transmits
only the model update (i.e., the learned model parameters) back to a central server. The central server then
combines the updates received from all the clients to form a single, improved model that represents the
knowledge gathered from the collective of the participants, while maintaining the confidentiality of each
participant's data.
This type of collaborative learning is particularly useful in cases where there are strict requirements for
the preservation of client data privacy and/or where client data is sensitive and should not be shared
publicly. Because no raw data is transmitted from the client to the server, federated learning protects client
data from breaches, misuses and unauthorized access. Furthermore, federated learning facilitates
compliance with client data privacy regulations such as GDPR. A further benefit is that federated learning
minimizes the amount of data that must be transferred across networks; instead of transferring large
volumes of data from client to server, federated learning enables clients to transmit only small updates to
the model.
Federated learning is being applied in a variety of real-world applications including predictive keyboards,
personalized product recommendations, smart health devices, and distributed IoT systems. An example of
federated learning in practice is Google's Gboard keyboard, which utilizes federated learning to create
better typing suggestions by combining knowledge from tens of millions of users without collecting their
actual typed messages. The idea behind federated learning is that every device contributes knowledge
from its data, while the central server only receives aggregated and anonymized improvements to the
model and not the original data.
Depending on the devices and organizations involved, federated learning can take several forms.
Cross-device federated learning involves a large number of personal devices, each containing small
amounts of varying-quality data. Cross-silo federated learning, on the other hand, involves a smaller
number of institutions (e.g., hospitals and banks) that collaborate to develop a common model without
sharing their respective sensitive datasets. While providing great opportunities for collaborative learning
and protecting data privacy, both approaches face similar challenges.
One of the main challenges facing federated learning is addressing non-identically distributed data, i.e.,
data on different devices, which can lead to unstable training processes. A second challenge lies in the
fact that some devices may frequently disconnect or participate sporadically, which presents particular
challenges in larger mobile networks. Finally, federated learning requires methods to securely aggregate
the model updates to prevent individual updates from being reconstructed and linked to a specific client.
Although federated learning still faces many technical challenges, it is developing rapidly and is
becoming increasingly important in creating privacy-preserving, scalable, and intelligent systems relying
on distributed data continues to evolve rapidly and is becoming a key technology for building
privacy-preserving, scalable, and intelligent systems that rely on distributed data.

<img width="2048" height="1096" alt="1" src="https://github.com/user-attachments/assets/537d6aa1-373f-43ee-b888-3bd322d874fe" />
*__Figure 1.__ The illustration is a mesh of clients each having their own data and each client sends model updates to other peer
clients that have a similar amount of data so they can learn together without a centralized server.*


```bibtex
@article{beutel2020flower,
  title={Flower: A Friendly Federated Learning Research Framework},
  author={Beutel, Daniel J and Topal, Taner and Mathur, Akhil and Qiu, Xinchi and Fernandez-Marques, Javier and Gao, Yan and Sani, Lorenzo and Kwing, Hei Li and Parcollet, Titouan and Gusmão, Pedro PB de and Lane, Nicholas D},
  journal={arXiv preprint arXiv:2007.14390},
  year={2020}
}
```

