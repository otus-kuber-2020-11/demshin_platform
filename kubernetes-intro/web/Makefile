USER_NAME=demshin

build_nginx:
	export USER_NAME=${USER_NAME} && docker build -t ${USER_NAME}/nginx .

push_nginx:
	docker push ${USER_NAME}/nginx

run_nginx:
	docker run -it --rm -d -p 8000:8000 --name web ${USER_NAME}/nginx