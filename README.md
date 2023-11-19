# Docker Compose Configuration

## Traefik and RabbitMQ Setup

This Docker Compose configuration sets up Traefik as a reverse proxy and RabbitMQ with management plugins. Traefik is used to handle SSL termination and route traffic to the RabbitMQ management interface.

### Prerequisites

Make sure you have Docker and Docker Compose installed on your machine.

### Usage

1. Clone this repository to your local machine.

2. Create a `.env` file in the same directory as your `docker-compose.yml` file with the following content, replacing placeholders with your actual values:

    ```env
    LETSENCRYPT_EMAIL=your-email@example.com
    RABBITMQ_USER=your-rabbitmq-username
    RABBITMQ_PASSWORD=your-rabbitmq-password
    APP_DOMAIN_URL=your-app-domain-url
    ```

3. Create the required directories for Traefik and RabbitMQ data:

    ```bash
    mkdir letsencrypt rabbitmq-data
    touch letsencrypt/acme.json
    sudo chmod 600 letsencrypt/acme.json
    ```

4. Run the Docker Compose command to start the services:

    ```bash
    docker-compose up -d
    ```

### Configuration Details

#### Traefik:

- Exposes ports: 80 (HTTP), 443 (HTTPS), 8080 (Traefik dashboard).
- Uses Let's Encrypt for SSL certificates.
- Routes traffic to RabbitMQ based on the specified domain.

#### RabbitMQ:

- Exposes the RabbitMQ management interface on port 15672.
- Sets RabbitMQ username and password as specified in the environment variables.
- Configures Traefik labels for routing and SSL termination.
- Persists RabbitMQ data on the host machine in the `rabbitmq-data` directory.

### Accessing Services

- Traefik Dashboard: http://localhost:8080
- RabbitMQ Management Interface: https://your-app-domain-url

### Notes

- Please make sure to secure sensitive information, such as passwords, in a production environment.
- Adjust the configurations as needed for your specific use case.
