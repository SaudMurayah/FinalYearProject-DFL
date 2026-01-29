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
*Federated Learning is a method of collaborative machine learning where multiple clients can collectively
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
privacy-preserving, scalable, and intelligent systems that rely on distributed data.*

<img width="2048" height="1096" alt="1" src="https://github.com/user-attachments/assets/537d6aa1-373f-43ee-b888-3bd322d874fe" />
Figure 1.The illustration is a mesh of clients each having their own data and each client sends model updates to other peer
clients that have a similar amount of data so they can learn together without a centralized server.

## ii. Literature Review
*The development of Federated Learning (FL) has been influenced by numerous developments in
distributed computing, privacy-preserving computations, and large-scale machine learning, which have
taken place over the last ten years. The early foundational work and subsequent research have shaped the
models, frameworks, and challenges that characterize current FL systems.
An important milestone was reached in 2017, when Google Research presented the first concrete
realization of a practical federated learning solution. They illustrated how machine learning models can
be trained cooperatively across millions of user-decentralized devices without exchanging the raw data.
Rather than transmitting raw data, only the updated model parameters were exchanged. This breakthrough
enabled the creation of the first practical, privacy-preserving, and communication-efficient learning
methods and marked the beginning of the development of FL as an attractive alternative to traditional
centralized training architectures.
In 2020 researchers at the University of Oxford collaborated with other industry partners to release
Flower, an open source platform for developing decentralized and flexible federated learning systems.
The open source platform Flower offered a modular architecture that was able to allow researchers to
experiment across different types of devices, network types and different training strategies. Due to
Flowers simplicity of use and ability to easily deploy a heterogeneous environment, it greatly aided in the
acceleration of research within decentralized and cross-silo FL systems.
Previous work done by McMahan et al. (2018) —also from Google— identified a fundamental problem
in Federated Learning: the communication bottleneck. They demonstrated through their research that
federated learning has to repeatedly communicate between clients and servers, and therefore in both
large-scale and bandwidth limited environments the communication cost can become prohibitive. The
cost of communication in federated learning led to additional research in the areas of communication
round reduction, efficient aggregation of client models and lossy compression of client updates to reduce
overhead.
A second critical research contribution to federated learning were the findings from the group at EPFL
(École Polytechnique Fédérale de Lausanne) in 2019 regarding the security vulnerabilities inherent to
federated learning systems. Their research found that federated learning systems are susceptible to
poisoning attacks where either malicious or compromised clients can purposefully submit poisoned model
updates to the global model. Poisoned model updates can result in a degradation of performance and/or
introduce hidden backdoors into the global model. The identification of these vulnerabilities in federated
learning systems motivated a substantial amount of research in the development of secure aggregation
methods, anomaly detection methods and robust optimization techniques to increase the trustworthiness
of federated learning environments.
The combined efforts of all three of the aforementioned contributions form the basis of today’s Federated
Learning research, demonstrating not only the potential benefits of Federated Learning, but also the
fundamental technological obstacles that continue to foster innovations within the Federated Learning
space including scalability, communication efficiency and security.*

## iii. Problem Statement
*A significant problem exists when trying to use the centralized training method in the distributed
environment of IoT and/or other similar big data applications. While there have been many successes
using the centralized training approach in traditional machine learning environments, it has many
problems that make it impractical for use in large, distributed systems. A major problem is the single
point of failure associated with centralized architectures. Because all of the data processing and
aggregation occurs at the central server, if the central server fails or is down due to hardware or network
issues, the entire training workflow will stop until the central server comes back online. Even a few
minutes of lost time during training can cause delays in updating models, decrease the overall reliability
of the system and increase the risk of operationally impacting an organization's ability to meet business
goals and customer expectations. Since the centralized architecture depends on a single component to
operate successfully, it does not lend itself well to being used in real world environments that can contain
thousands to millions of devices sending data to the system.
Another major issue with centralized architectures is that they quickly run into scalability challenges once
there are many more nodes in the system than the number of cores available in the central server. Each
node sends either the raw data or training results directly to the central server which creates a significant
amount of communications traffic. Therefore, as more nodes are added to the system, the server becomes
a bottleneck for communications and can have difficulty handling the large amounts of data exchange.
Oftentimes, this results in longer latencies between the nodes, slower rates of model convergence, and
lower efficiency, particularly in very large-scale applications such as IoT networks, mobile devices, and
distributed sensor environments. Furthermore, the central server requires significantly more hardware and
bandwidth to support additional nodes and therefore is costly to scale and difficult to maintain.
Beyond performance issues, centralized systems also face concerns related to privacy, energy
consumption, and fairness across nodes, further showing that this approach becomes less practical as data
grows more decentralized. These limitations highlight the need for alternative training methods—such as
federated learning—that distribute computation, reduce server load, and eliminate single points of failure.
In addition to performance issues, centralized architectures also have serious drawbacks regarding issues
of privacy, power usage, and fairness among the nodes. Therefore, as the decentralized nature of the data
continues to grow, the centralized architecture continues to lose viability as a viable solution.
Overall, these issues highlight the need for new ways of training models—ways such as decentralized
federated learning—that will allow for computation to be distributed away from the central server,
provide for reduction of the server load, and remove the single point of failure inherent in the centralized
architecture.*

<img width="742" height="430" alt="2" src="https://github.com/user-attachments/assets/42c2e397-7f2d-4809-96c6-6a421d989e86" />
Figure2. Illustrates how in the classic federated learning topology there is one main or central server and many clients. Each
client trains on their own data and sends it back to the central server to be aggregated. The central server then uses these
updated models to train its own model which is then sent out to all the clients again

## iii Objectives
This project aims to develop a scalable P2P communication network that eliminates the
central bottleneck. Specifically, the objectives of this project include:
- Develop a communication system where clients can communicate directly via gRPC.
- Implement decentralized model aggregation and gossip-based propagation.
- Measure scalability and convergence rate relative to baselines of centralized approaches.

## iv. Functional and Non-Functional Requirements
### iv.i Functional requirements
- Communication of Client:
Each client must be able to dynamically find and establish a connection to other peers.
Topology of System Support for various types of topologies (Mesh, Hybrid, etc.).
- Training & Update Models:
Each client trains independently a local version of the model.
Secure Exchange and Aggregation of Updates
Updates for the model should be exchanged securely and aggregated.
- Fault Tolerant Synchronization:
The system must be able to manage node failures and inconsistencies in model updates.
### iv.ii Non-Functional Requirements
- Scalability: Support a large number of clients.
- Performance: Minimize latency in exchange of models.
- Reliability: Ability to tolerate partial failures.
- Compliance: Ensure compliance with privacy regulations (e.g., GDPR).

```bibtex
@article{beutel2020flower,
  title={Flower: A Friendly Federated Learning Research Framework},
  author={Beutel, Daniel J and Topal, Taner and Mathur, Akhil and Qiu, Xinchi and Fernandez-Marques, Javier and Gao, Yan and Sani, Lorenzo and Kwing, Hei Li and Parcollet, Titouan and Gusmão, Pedro PB de and Lane, Nicholas D},
  journal={arXiv preprint arXiv:2007.14390},
  year={2020}
}
```

