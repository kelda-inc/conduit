build-django:
	cd ../backend && docker build -t keldaio/conduit-django .

build-react:
	cd ../frontend && docker build -t keldaio/conduit-react .

push-django: build-django
	docker push keldaio/conduit-django

push-react: build-react
	docker push keldaio/conduit-react
