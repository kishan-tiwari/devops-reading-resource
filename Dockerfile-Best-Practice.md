# Docker BuildKit: builder v2
- concurrency, lazy context, upload, better caching, new dockerfile features...

# Use latest Docker, enable builkit 
## docker client:
- export DOCKER_BUILDKIT=1

## Or, docker daemon config:
- {
	"features" :  {"buildkit" : true}
}

# Improving Dockerfiles 
## Areas of improvements
- (Incremental)  build time
- Image size
- Maintainability 
- Security
- Consistency/Repeatability


# Remove unnecessary dependecies 
- use apt-get -y install --no-install-recommends openjdk-8-jdk

# Remove package manager cache 
- rm -rf /var/lib/apt/lists/*

# Use official images where possible 
- Reduce time spent on maintenance (frequently updated with fixes)
- Reduce size (shared layers between images)
- Pre-configured for container use
- Built by smart people 

# Project with many stages 
- https://github.com/moby/moby/blob/master/Dockerfile
- https://mobyproject.org/

# Building specific stages with  --target 
- FROM image_or_stage AS stage_name
- docker build --target stage_name

# Various environments: build, dev, test, lint, ...
## Examples of possible stage layout:
- builder: all build dependecies
- build (or binary): builder + build artifacts 
- cross: same as build but for multiple platforms
- dev: build(er) + dev/debug tools
- lint: minimal lint dependencies
- test: all test dependencies + build artifacst to be tested
- release: final minimal image with build artifacts 

# New Dockerfile features
- https://github.com/moby/buildkit/blob/master/frontend/dockerfile/docs/experimental.md
- https://github.com/moby/buildkit/blob/master/docs/experimental-syntaxes.md

# Pass ARG at the time of docker image build
- docker build --build-arg AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID

# Advanced multi-stage build patterns
- https://medium.com/@tonistiigi/advanced-multi-stage-build-patterns-6f741b852fae
- https://medium.com/@tonistiigi/build-secrets-and-ssh-forwarding-in-docker-18-09-ae8161d066






























