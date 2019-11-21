docker build -t hiloimg .
docker run --name runninghilo --rm -p 8080:8080 hiloimg

# iron/go:dev is the alpine image with the go tools added
FROM iron/go:dev
WORKDIR /app
# Set an env var that matches your github repo name, replace treeder/dockergo here with your repo name
ENV SRC_DIR=/go/src/github.com/gmac220/hellogo/
docker run --rm -v "$PWD":/go/src/github.com/gmac220/hellogo -w /go/src/github.com/gmac220/hellogo iron/go:dev go build -o thisapp

docker build -t hiloimg .

docker run --name runninghilo --rm -p 8080:8080 hiloimg

# make a docker repo & running

docker login

docker tag hiloimg godfrey220/hellogo:v1

docker push godfrey220/hellogo:v1

docker run --rm -it -p 8080:8080 godfrey220/hellogo:v1

hellos