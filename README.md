# Decentralized Federated Learning For Enhancing Scalability & Resilience

## Abstract
In traditional Federated Learning (FL), an aggregator server collects and coordinates updates
from client machines, resulting in a potential bottleneck in scalability and a single point of
failure. This project aims to evaluate the feasibility of Decentralized Federated Learning (DFL)
to utilize peer-to-peer (p2p) communication among clients to provide both high-performance and
resilient system architecture. Using a modified version of the flower framework to implement
gRPC protocol, this project allows client updates to flow directly to other clients without an
intermediary aggregator server. Results of experiments conducted with the MNIST dataset show
that our DFL architecture is capable of achieving model convergence, yielding an increase in
accuracy from 14% to 33% during three rounds of training while decreasing reliance on a
central aggregator server.

## TABLE OF CONTENT
   Abstract
1. Introduction
2. Literature Review
3. Problem Statement & Objectives
4. Functional and Non-Functional Requirements
5. System Architecture and Design
6. Methodology and Implementation Details
7. Experiments and Result Analysis
8. Challenges and Discussions
9. Conclusion & Future Work
References



```bibtex
@article{beutel2020flower,
  title={Flower: A Friendly Federated Learning Research Framework},
  author={Beutel, Daniel J and Topal, Taner and Mathur, Akhil and Qiu, Xinchi and Fernandez-Marques, Javier and Gao, Yan and Sani, Lorenzo and Kwing, Hei Li and Parcollet, Titouan and Gusmão, Pedro PB de and Lane, Nicholas D},
  journal={arXiv preprint arXiv:2007.14390},
  year={2020}
}
```

