# iron/go:dev is the alpine image with the go tools added
FROM iron/go:dev
WORKDIR /app

#RUN yum install -y git

RUN go get github.com/gin-gonic/gin

RUN mkdir -p /go/src/github.com/sumitg/

# Set an env var that matches your github repo name, replace treeder/dockergo here with your repo name
ENV SRC_DIR=/go/src/github.com/sumitg/loans-app

RUN cd /go/src/github.com/sumitg/ && git clone https://github.com/sumitg/loans-app.git loans-app

# Build it:
RUN cd $SRC_DIR; go build -o main; cp main /app/; cp -R templates /app/;
ENTRYPOINT ["./main"]

