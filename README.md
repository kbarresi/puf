# puf
puf (Painless Update Framework) is a cross platform application update framework written in C++.

I tried to make puf as simple as possible to integrate into new or existing projects, while still having a lot of functionality. puf requires a web server to pull updates from, and I included a Node.js application that does the job. See the server/ directory for more information on that.


== Overview 

puf is written in C++ using the Qt framework for networking and GUI components. The goal of this project is to complete the following deliverables:

  * Easy integration into client applications
  * Minimize network usage
  * Perform update checking and preparation without affecting application performance
  * Submitting new updates should be really easy
  * Provide a decent level of customization without being overwhelming


With these requirements in mind, I chose the following strategies:

  * Clients start the updater with a one-liner, with optional callbacks.
  * The client will start the updater process, and the updater process will outlive the client process.
  * Clients can specify a platform and “variant” identifier when requesting updates.
  * We use server-side file deltas to calculate what update files are needed.
  * Our updater runs as a separate process, with its own UI capabilities and event loop.
  * The updater communicates with the client process via local sockets/named pipes.
  * Updates are submitted by uploading a .zip file containing new files and update information.
  * Update information in the .zip file is in JSON format.
  * The server is a Node.js RESTful API.