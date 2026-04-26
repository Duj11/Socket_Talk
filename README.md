# SocketTalk Campus Messenger
A real-time desktop chat app built in Java where users can message each other, see who's online, and admins can manage accounts.

## Features
- Real-time private messaging over TCP sockets
- User login and registration
- Online/offline status indicators
- Chat history that saves and loads between sessions
- Admin panel for managing users and viewing stats
- Auto-generated colour avatars per user

## Technologies Used
- Java
- JavaFX (UI)
- TCP Sockets

## The Process
- The server listens for connections and spins up a new thread for each user that joins. A shared map keeps track of who's online so messages can be routed to the right person instantly.
- Messages between the client and server are just plain strings separated by a `|` character — something like `MSG_PRIVATE|bob|Hey!`. The server splits that string and figures out what to do based on the first part.
- User accounts are saved in a simple text file. Chat history is saved per conversation in its own file, with a naming convention that stays consistent no matter who sends first.
- On the client side, a background thread handles all incoming messages so the UI never freezes. Any time the UI needs to update from that thread, it gets handed off safely to the JavaFX thread.
- User avatars are coloured based on the user's ID, so everyone always gets the same colour without needing to store it anywhere.

## Preview 
![App Screenshot](assets/screenshots/screenshot1.png)
![App Screenshot](assets/screenshots/screenshot2.png)
![App Screenshot](assets/screenshots/screenshot3.png)

## What Was Learned
- How to manage multiple users connecting at the same time without things breaking — using synchronized methods and thread-safe data structures.
- Keeping the network code and the UI code separate so they don't get tangled up, and safely passing data between background threads and the UI.
- Building a simple custom messaging protocol from scratch and the quirks that come with parsing it.
- Handling persistent storage with just plain files in a way that stays consistent across sessions.

## Future Plans
- Swap the text file storage for an actual database
- Message read receipts
