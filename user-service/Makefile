all: build run

build:
	@echo "Building~~~~~~~~~~~~~~~~"

	protoc -I . --go_out=plugins=micro:$(GOPATH)/src/github.com/howl-io/shippy/user-service proto/user/user.proto

	GOOS=linux GOARCH=amd64 go build

	docker build -t user-service .

run:
	@echo "Runing~~~~~~~~~~~~~~~~~~~"

	docker run -p 50053:50051 \
		-e MICRO_SERVER_ADDRESS=:50051 \
		-e MICRO_REGISTRY=mdns \
		-e MICRO_BROKER_ADDRESS=0.0.0.0:4222 \
		user-service

.PHONY: all build run
