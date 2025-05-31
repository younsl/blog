

serve:
	podman run --name slidev \
	 --rm -it \
	 --user node \
	 -p 3030:3030 \
	 -v ${PWD}:/slidev \
	 tangramor/slidev:latest

open:
	open http://localhost:3030