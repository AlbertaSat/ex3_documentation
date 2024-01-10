# Simulated subsystem architecture

-------------------------------------------

## Subsystem high level architecture diagram

![High level simulated subsystem architecture](imgs/AlbertaSat_ExAlta3-Simulated_Subsystem_Architecture_v3.png)

## Brief explanation of architecture

### Sim subsystems

- Do subsystem specific things only such as managing internal subsystem state, and implementing specific functionality unique to the subsystem.
  Subsystems ignore implementation specifics for the communication interface such as 'I2C vs SPI vs CAN etc'.
- Each subsystem should be able to receive and emit messages. Because all subsystem will communicate in various ways, each subsystem simulated should have an example of the types of messages it expects to receive, and send send, along with a breif description of their format and function.
- All messages sent and received are logged by the individual subsystem upon receive and send.
- Data may be piped between subsystem components backend and other software or apis.

#### Subsystem / payload message structure

- Each subsystem / payload has a unique message format/structure and thus is responsible for deconstructing incomming messages from the OBC, and constructing outgoing message to the OBC. This is because in reality most subsystems are third party devices which act like a black box and thus use their own unique message structure for control and emission of messages / notifications.
- The structure of the message for each subsystem should be somewhat similar with what is expected for the actual subsystem.

### Sim Satelllite Manager

- Responsible for beginning the entire simulated satellite ecosystem. The satellite ecosystem manager brings all the simulated subsystem modules together.
- Spawns each subsystem / payload (TBD if each subsystem is spawned as a seperate process or thread).
- Central control allows subsystems processes to be started / killed together or inidividually for testing. Allows entire 'configurations' of the satellite eco system to be saved, and used for testing.
- Simplifies potential future implementation of a subsystem / simulated satellite ecosystem GUI.
- May be used to establish connections to backend of each subsystem such as programs to generate realistic simulations data for things like the ADCS etc.
- Can be used to test boot up and other satellite wide operations.

### Subsystem Interfaces

- OBC FSW modules which act as interfaces / drivers to communicate with an associated subsystem. Also isolates communication handling from application specific module code. Before ICDs are provided by the associated subsystems / payloads TCP sockets will be used. The interface / driver modules in the FSW for each subsystem / payload will be responsible for managing a unique socket for each.

### External APIs, Simulators, Data sources

- The back end of this simulated satellite manager may be configured to interface with APIs for a variety of reasons to make the simulated satellite ecosystem more useful.
- For example a mod that uses an API to communicate with Kerbal Space Program may be used to provide data to the simulated subsystem components and OBC to demonstrate the satellites operation in various settings that can be setup easily in game.