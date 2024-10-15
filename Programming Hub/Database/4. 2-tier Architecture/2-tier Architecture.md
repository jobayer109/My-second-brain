![[2-tier.png]]


#### Definition
2-tier architecture is a client-server model where the client directly interacts with the database server.

#### Components
1. **Client**:
   - Front-end application for user interaction.
   - Handles presentation logic and user input.
   - **Examples**: Desktop applications, web browsers.

2. **Server**:
   - Back-end system for data processing.
   - Manages database access and storage.
   - **Examples**: MySQL, Oracle, SQL Server.

#### Workflow
1. Client sends a request to the server.
2. Server processes the request and accesses the database if needed.
3. Server returns processed data to the client.

#### Advantages
- **Simplicity**: Easy to develop and maintain.
- **Performance**: Faster communication between client and server.

#### Disadvantages
- **Scalability**: Limited due to direct interactions.
- **Security**: Direct database connection poses risks.
- **Maintenance**: Database schema changes require client updates.

#### Use Cases
- Small to medium-sized applications.
- Desktop applications with local database access.
- Simple client-server web applications.

#### Summary
2-tier architecture is suitable for straightforward applications, balancing ease of development with performance, but may face challenges in scalability and security for larger systems.