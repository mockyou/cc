

After you've pushed files, follow this on your EC2 instance:

```bash
sudo apt update
sudo apt install git -y
git clone https://github.com/mockyou/portfolio.git
cd portfolio
```

Create a **Dockerfile** (if not already there):

```dockerfile
# Dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

Install Docker:

```bash
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
```

Build the Docker image:

```bash
sudo docker build -t mockyou/htmlpage .
```

Run the container:

```bash
sudo docker run -d -p 80:80 mockyou/htmlpage
```

Visit `http://<your-EC2-public-ip>` in your browser to see your page live.

---

