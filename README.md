# how_to_deploy

poetry add streamlit
poetry add fastapi
poetry add sqlalchemy


Basic Operations
- `streamlit run app.py`
- `uvicorn main:app --reload`



# Heroku


無料用Dyno

設定時は、dyno sizeの「Free」が選択肢に出てこなくて、「え？これ有料のDynoじゃね？」と思いつつ「Standard-1X」にしてみました。
しかし、1度でも実行すると管理画面で「Free」に表示に変わりました。


# Docker

### Host OS & Guest OS  
- Host OS: The operating system running on your computer (Windows, macOS, Linux). It runs Docker.
- Guest OS: The system inside the container (like Ubuntu, MySQL). It shares the Host OS kernel.

### Docker Hub
Docker Hub is a library of container images. You can pull images to your local machine.
https://hub.docker.com/

### Command List with Command Prompt

| Command | Description | Options & Explanation |
|---------|------------|----------------------|
| `docker pull mysql` | Download the MySQL image to your local machine. | - |
| `docker images` | List all downloaded images. | - |
| `docker run --name some-mysql -p 13306:3306 -e MYSQL_ROOT_PASSWORD=my-secret-pw mysql` | Start a MySQL container. | `--name some-mysql` → Assigns a name to the container. <br> `-p 13306:3306` → Maps port **13306** on the host to **3306** inside the container. <br> `-e MYSQL_ROOT_PASSWORD=my-secret-pw` → Sets MySQL root password as an environment variable. |
| `docker ps` | Show running containers. | - |
| `docker exec -it container_name bash` | Enter a running container. | `-it` → Interactive mode (use the container like a terminal). |
| `mysql -u root -p` | Login to MySQL inside the container. | `-u root` → Username (`root`). <br> `-p` → Prompt for password. |
| `docker stop container_name` | Stop a running container. | - |
| `docker ps -a` | Show all containers (running & stopped). | `-a` → Show stopped containers list as well. |
| `docker start container_name` | Restart a stopped container. | - |
| `docker rm container_name` | Delete a container. | - |
| `docker rmi image_name:version` | Delete an image from local storage. | - |

### Example for the docker file
```
FROM ubuntu:20.04

# Update and install packages
RUN apt update
RUN apt install -y python3.9
RUN apt install -y python3-pip

# Copy required files
COPY requirements.txt .
RUN python3.9 -m pip install -r requirements.txt

# Set environment variable
ENV SITE_DOMAIN=palakpaneer.com

# Set working directory
WORKDIR /var
```
- FROM ubuntu:20.04: Uses Ubuntu 20.04 as the base image.
- RUN: Runs commands inside the container (install software).
- COPY: Copies files from the host to the container.
- ENV: Sets environment variables.
- WORKDIR: Sets the working directory inside the container.  
Command-List for Docker file
https://docs.docker.com/reference/dockerfile/


Build a Container from Dockerfile (using Command Prompt)
```docker build -t container_name -f /path/to/Dockerfile .``` 


