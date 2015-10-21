# dfuzz
distributed deep binary fuzzer...

This system has five main different subsystems.

1. Distribution
   A NanoMSG component that communicates with MySQL.  It loads all of the operations into memory for scalability.  It's created
   for use with tens of thousands of fuzzing clients.  It opens nanomsg listeners for the HTTP webserver portion, and
   for the linux fuzzing clients.

2. HTTP (Nginx module)
   It communicates with the distribution component via nanomsg.  It allows clients to upload, or download information via HTTP.
   
3. Fuzz Client
   Downloads information from the distributor.  It will fuzz a specific set of instructions with a particular range, and report
   back to the distributor with the results.
   
4. The analyzer
   This executes the initial run of the software.  It creates the particular packages which are uploaded to the distributor.
   It does most of the analysis.  The fuzz client uses a lot of the same code, but doesn't require all of it.
   
5. API Proxy Server
   This runs on a real windows machine.  It allows the fuzzing analyzer to retrieve real values back from windows.  This allows
   deep fuzzing without replicating all windows API.
