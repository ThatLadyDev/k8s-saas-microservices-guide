# Detailed instructions for setting up the services locally

This guide provides the necessary steps to set up the microservices project locally using Docker Compose. I’ve also included a `Makefile` to automate necessary tasks for easier setup and management.

## **Prerequisites**

Ensure you have the following installed:

1. **Docker**  
   [Install Docker](https://docs.docker.com/get-docker/)

2. **Docker Compose**  
   [Install Docker Compose](https://docs.docker.com/compose/install/)


## **Setup Instructions**

### 1. **Clone the Repository**

Start by cloning the repository containing the mircorservices local environment:

```bash
git clone git@github.com:ThatLadyDev/k8s-saas-local-environment.git
cd your-repository
```

### 2. **.env file Creation**

The project requires environment variables to be set up via the `.env` file. To create your local `.env` file, run the following command:

```bash
cp .env.example .env
```
This will create the `.env` file based on the default settings provided in `.env.example`. You can update the `.env` file as needed for your local environment.

### 3. **Using the Makefile**

This project includes a Makefile to simplify setup and common tasks. Below are the most commonly used commands.

### **Available Commands**
| Command                  | Description                              |
|--------------------------|------------------------------------------|
| `make setup-services`    | Sets up the whole project and its services locally.                    |
| `make build`             | Builds the needed docker iamges and starts the containers in the background. |
| `make start`             | Runs all the containers in the background.            |
| `make stop`              | Stops all running containers.   |

![image](https://github.com/user-attachments/assets/f82bda29-aa14-4639-ab89-29d4b3bdae58)

### 4. **Start the Project**

Run the following commands to build and start the containers:

```bash
make setup-services
```

This will:
- Pull all the backend microservices from GitHub.
- Pull and build the Docker images for all the microservices.
- Start all services in the background.

### 5. **Testing the Setup**

To verify the setup, open your browser and input the following in the URL box `http://localhost:8080`. Here’s an example of how it should look like:
![image](https://github.com/user-attachments/assets/e1bc395b-53d1-45af-b363-adc5cbf506ed)


You’re all set! 🚀 If you encounter any issues, feel free to ask for help or check the logs for debugging.
