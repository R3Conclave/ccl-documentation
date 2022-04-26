# What is Conclave Cloud?
Conclave Cloud is a platform for hosting privacy-preserving applications. Built
on top of the Conclave SDK, which in turn is built to take advantage of Intel
Software Guard Extensions (Intel SGX), Conclave Cloud is a platform that will
provide all the tools necessary to ensure that access to data is provided only
to authorised parties.

The Conclave Cloud platform will bring together an expanding set of services
that will seamlessly integrate with each other providing a rich set of tools for
implementing solutions without ever having to leave the Conclave Cloud platform.

![](../../../Meetings/Conclave%20Offsite%20Q2%202022/ImmersiveEcosystem-CCL.drawio.png)

But we're not there yet! We don't have all of the services in the diagram above
in the platform. In fact, we will be relying on our customers (including you) to
drive the requirements for which services we should prioritise.

### So what services _does_ Conclave Cloud deliver now?
The current platform delivers our first service, Conclave Functions, which is a
serverless execution environment, much like AWS Lambda or Azure Cloud Functions.

Conclave Functions differs from other similar services by using end-to-end
encryption between the end user and the container that runs the function, with
data-in-use encryption provided by using a Conclave Enclave to run the code. The
use of an enclave ensures the integrity and privacy of the user's data as well
as providing hardware-backed assurances over the exact code that will be
processing the data.

With Conclave Functions, developers can deploy their code once to the platform
where it will then be hosted for them. Their functions can be called once a
year, once an hour, up to thousands of times an hour. The platform will cope
with the demand and scale accordingly with no management or intervention from
the developer.

## What can you do with Conclave Cloud/Functions?
Conclave Functions allows you to write code that will run inside an enclave with
_absolutely no boilerplate whatsover_! This means that you can focus on writing
your data processing logic that will run inside an enclave without worrying
about how to transfer data to and from the enclave, or how to encrypt data, or
how to ensure the platform integrity is maintained.

You can prove to your users that the code that you say will process their data
actually is the code that processes the data, as well as proving that you as a
service host or author do not have access to the keys that encrypt the user's
data. In fact, it also proves that _nobody except the Conclave Functions enclave
can access the data_, and that includes R3 and Azure: our cloud service
provider.

Theoretically, any problem that can be solved using the Conclave SDK can also be
solved in Conclave Functions. However, features such as persistence and
authentication will be provided by additional services in the platform that do
not yet exist.

One thing to remember is that Conclave Functions are stateless. Every time you
invoke your function in the Conclave Functions service, any previous state is
likely to be lost. There is a chance that previous state is available in-memory
but you cannot rely on it - the best you can do is use any previous state as a
cache that can be used if present.

Obviously stateless functions have limited use - you may as well just run the function
locally on the user's machine if you don't have the ability save or share data
from the cloud.

Luckily, Conclave Functions provides an alternative to storing state directly.
It supports a subset of the JavaScript `fetch()` API allowing outgoing calls to
external services. This means that a function can retrieve and set data using an
external service. Care must be taken to ensure private data is not leaked by the
external call, as the actual call takes place outside of the enclave.

## But what problems can be solved with Conclave Functions?
Conclave functions can be used to provide solutions or enhance the privacy for
many different types of application, including:

* Pure data protection products such as cloud-based file storage with secure
  file sharing.
* Zero Knowledge Proof type applications, such as proving identity or age
  without providing the actual data to the verifying party.
* Multiparty computation where data is collated from multiple parties and
  derived into a combined result, without divulging the shared data with any
  other party or service.
* Private set intersection applications, such as allowing different
  institutions to find common data between their own private datasets and the
  data of other parties.

Conclave Cloud provides a sample which shows how to implement a password manager
using Conclave Functions along with a web-based frontend, a Kotlin-based CLI
tool and a Spring backend for persistence. You can find the sample in [this
GitHub repository](https://github.com/R3Conclave/ccl-sample-conclavepass). The
sample does not really fit into any of the categories above, but you can imagine
expanding it to allow, for example, the service to automatically scan for
compromised keys and notify the user.