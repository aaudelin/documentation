# Les couches du modèle OSI

[Documentation stack overflow](https://stackoverflow.com/questions/38596488/in-which-layer-is-http-in-the-osi-model)

## The OSI model

The OSI (Open Systems Interconnection) model is a conceptual model created by the International Organization for Standardization which enables diverse communication systems to communicate using standard protocols.

It provides a standard for different computer systems to be able to communicate with each other and can be seen as a universal language for computer networking. It’s based on the concept of splitting up a communication system into seven abstract layers, each one stacked upon the last.

The following picture [borrowed from Cloudflare][3] illustrates pretty well what the OSI model is like:

[![The OSI model][4]][4]

The application layer is the only layer that directly interacts with data from the user. So software applications like web browsers and email clients rely on the application layer to initiate communications.

But it should be made clear that client software applications _are not part of the application layer_: rather the application layer is responsible for the protocols (such as HTTP and SMTP) and data manipulation that the software relies on to present meaningful data to the user.

## The OSI model vs the TCP/IP model

While the OSI model is comprehensive reference framework for general networking systems, it's important to mention that the modern Internet doesn’t _strictly_ follow the OSI model.

The modern Internet more closely follows the simpler _Internet protocol suite_, which is commonly known as _TCP/IP_ because the foundational protocols in the suite are the _TCP_ (Transmission Control Protocol) and the _IP_ (Internet Protocol).

The following image illustrates how the OSI and TCP/IP models relate to each other:

[![OSI model vs TCP/IP][5]][5]

  [1]: https://tools.ietf.org/html/rfc7230
  [2]: https://tools.ietf.org/html/rfc6265
  [3]: https://www.cloudflare.com/learning/ddos/glossary/open-systems-interconnection-model-osi/
  [4]: https://i.stack.imgur.com/WG5r8.jpg
  [5]: https://i.stack.imgur.com/ysG0q.jpg
