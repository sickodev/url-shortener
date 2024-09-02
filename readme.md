# URL Shortener Service

This project is a Dockerized URL Shortener service written in Go that uses Redis as the backend for storing shortened URLs. The service allows users to shorten URLs by passing a custom ID or having one generated randomly. It includes fault prevention mechanisms, rate limiting, and other security measures to protect against attacks.

## Features

-   **Custom and Random ID Support**: Users can provide their own custom ID for the shortened URL, or the service can generate a random ID if none is provided.
-   **Redis Backend**: URLs are stored in Redis, providing fast and efficient lookups.
-   **Fault Prevention**: The service includes mechanisms to handle errors gracefully, ensuring that it remains robust and reliable.
-   **Rate Limiting**: Rate limiting is implemented to prevent abuse and ensure fair usage of the service.
-   **Dockerized**: The service is fully Dockerized, making it easy to deploy and run in any environment.

## Prerequisites

-   **Docker**: Ensure that Docker is installed on your machine.
-   **Go**: If you want to run the service without Docker, you need Go installed on your machine.
-   **Redis**: The service relies on Redis, which can be run as a Docker container or installed natively.

## Getting Started

### Clone the Repository

```bash
git clone https://github.com/sickodev/url-shortener.git
cd url-shortener
```

### Running the Service with Docker

1. **Build the Docker Image**

    ```bash
    docker build -t url-shortener .
    ```

2. **Run Redis and the URL Shortener Service**

    ```bash
    docker-compose up
    ```

    This will start both the Redis container and the URL Shortener service.

### Running the Service without Docker

1. **Install Redis**

    Ensure Redis is installed and running on your system.

2. **Build the Go Application**

    ```bash
    go build -o url-shortener main.go
    ```

3. **Run the Application**

    ```bash
    ./url-shortener
    ```

### Configuration

The service can be configured via environment variables:

-   `DB_ADDR`: The hostname of the Redis server (default: `localhost:6379`).
-   `API_QUOTA`: The number of requests allowed per minute (default: `10`).

These can be set in the `.env` file or passed directly into the Docker container using `docker run -e`.

## API Endpoints

### Shorten a URL

-   **POST** `/shorten`

    Request Body:

    ```json
    {
        "url": "https://example.com",
        "custom_id": "example" // optional
    }
    ```

    Response:

    ```json
    {
        "shortened_url": "http://localhost:3000/example"
    }
    ```

    If `custom_id` is not provided, a random ID will be generated.

### Redirect to the Original URL

-   **GET** `/{id}`

    This endpoint will redirect the user to the original URL associated with the given ID.

### Error Handling

-   **404 Not Found**: If the provided ID does not exist.
-   **400 Bad Request**: If the input is invalid.
-   **429 Too Many Requests**: If the rate limit is exceeded.

## Security Features

-   **Rate Limiting**: Limits the number of requests per minute to prevent abuse.
-   **Input Validation**: Ensures that all inputs are properly validated to prevent injection attacks.
-   **Fault Prevention**: Implements mechanisms to handle unexpected errors gracefully.

## Contributing

Contributions are welcome! Please submit a pull request or open an issue if you have any improvements or bugs to report.

## Contact

For any questions or support, please contact [kalyanbishwa03@gmail.com](mailto:kalyanbishwa03@gmail.com).
