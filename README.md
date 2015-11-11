** NOTICE: dfuzz, and it's modules will become public again at the next actual 'release' which will be soon.  It'l be a completed version with ability to pick an application, start a server process, and automatically begin fuzzing.  It will also have a client that has the ability to use a server configuration so you can add fuzzing power.

# dfuzz
distributed deep binary fuzzer...

This system has five main different subsystems.  Each has its own repository and is as a submodule..

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

6. PIDDUMP - Fuzzing Instruction Dumper
   If you don't want to begin with the emulator.  Set some breakpoints on functions such as ReadFile, recv() from       Winsock and every time a breakpoint hits then it will dump a fuzzing context to disk for insertion into the 
   database.
