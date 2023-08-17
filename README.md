# Scotland-Yard

We were given ManualPlayer.java and RandomPlayer.java. A process running the main method of either of these files is what we call a Client. The Client establishes a socket connection to the game Server (that’s the process running the main method of ScotlandYard.java) that listens on a port.

The client code basically listens for incoming input from the connection with a BufferedReader, and then decides on a move (either gets it from a human typing on the terminal, or generates it randomly), and sends that move across to the server with the PrintWriter associated with the socket connection.

The Server, on the other hand, caters to several clients, who are playing a single game. For multiple clients, the way to go is to spawn threads, one for serving each client, and then continue listening again.

Our server is organised as follows: we have a few ports that we can specify on the command line. For each port, the server loops: spawning a ScotlandYardGame and letting it run to completion. It is the ScotlandYardGame that listens on a port for client connections.

For each client that connects via a socket, we create a ServerThread to talk to it. This ServerThread facilitates round by round play. ServerThreads playing the same game have shared access to the same Board, and need to access data consistently and run in synchrony.

Finally, we also have the Moderator, whose primary job is to allow ServerThreads into the next round.
