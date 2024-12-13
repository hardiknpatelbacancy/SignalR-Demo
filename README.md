# SignalR Demo with ASP.NET Core MVC

This project demonstrates the implementation of **SignalR** in an ASP.NET Core MVC application using .NET 8. It includes features like real-time messaging, user groups, and private messaging.

## Features

- **Real-Time Messaging**: Broadcast messages to all connected clients.
- **User Groups**: Manage communication between specific sets of users. (WIP)
- **Private Messaging**: Send direct messages between users. (WIP)

## Prerequisites

- .NET 8 SDK
- Visual Studio 2022 or Visual Studio Code
- Node.js (for front-end package management, if needed)

## Getting Started

### 1. Clone the Repository
```bash
git clone (https://github.com/hardiknpatelbacancy/SignalR-Demo.git)
cd signalr-demo
```


### 2. Build the Project
Restore the NuGet packages and build the project:
```bash
dotnet restore
dotnet build
```


### 3. Run the Application
Run the application locally:
```bash
dotnet run
```

The application will start at `http://localhost:5000` (or another port as specified in the console).

### 4. Test Real-Time Features
Open the application in multiple browser tabs or different devices to test real-time communication.

## Implementation Details

### SignalR Integration

#### Server-Side
- SignalR services are added in `Program.cs`:
  ```csharp
  builder.Services.AddSignalR();
  app.MapHub<ChatHub>("/chatHub");
  ```
- `ChatHub` handles messaging, group management, and private messaging.

#### Client-Side
- SignalR JavaScript library is included via CDN:
  ```html
  <script src="https://cdnjs.cloudflare.com/ajax/libs/microsoft-signalr/7.0.0/signalr.min.js"></script>
  ```
- JavaScript manages connections and real-time events.

### Key Functionalities

#### Broadcasting Messages
Messages are sent to all connected clients:
```csharp
await Clients.All.SendAsync("ReceiveMessage", user, message);
```

#### User Groups
Users can join or leave groups and send group-specific messages:
```csharp
await Groups.AddToGroupAsync(Context.ConnectionId, groupName);
await Clients.Group(groupName).SendAsync("ReceiveMessage", user, message);
```

#### Private Messaging
Direct messages are sent using `ConnectionId`:
```csharp
await Clients.Client(connectionId).SendAsync("ReceiveMessage", "Private", message);
```

## Contributing

Contributions are welcome! Please fork the repository and submit a pull request for any changes.
