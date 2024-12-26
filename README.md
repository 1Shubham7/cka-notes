# cka-notes

![340174607-b1bfe6ae-a1e6-4b04-8486-272d3ed380bc](https://github.com/user-attachments/assets/fa9c49d6-181f-48ad-ba2b-031f605feb82)

### Docker Multi-stage builds tips 

- Use Official Base Images: Start with minimal base images like alpine or distroless when possible.
- Separate build-time and runtime dependencies to keep the final image lightweight.
- Use .dockerignore to exclude files and directories not needed in the build context.
- Order Instructions Strategically: Place less frequently changing commands first to leverage layer caching effectively.
- Use && or multi-line scripts in a single RUN instruction to reduce the number of layers.
- Remove package cache files and unnecessary dependencies after installation (e.g., apt-get clean or rm -rf /var/lib/apt/lists/*).
- Install only the libraries and tools needed for the application to run.
- Avoid installing unnecessary debugging tools in production images.


## Imp Questions

1. for python app we need a python runtime, but for go app we dont need a go runtime why?
2. Why multi stage builds?
3. what are distroless images
