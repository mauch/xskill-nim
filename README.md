# xskill-nim
Notebook and data for NVIDIA-NIM cross skilling session

To run the notebook setup the environment in conda using:

`conda env create -f environment.yml -p ./xskill-rag`

then:

`conda activate ./xskill-rag`

then start a notebook server and load the notebook in the browser:

`jupyter notebook`


# How to set up a NIM for `llama-3.1-8b-instruct` on MPC:

1. Go to: https://org.ngc.nvidia.com/setup/personal-keys and set up an API key (also create an NVIDIA Account if it doesn't already exist).
2. When creating an NGC API key, ensure that at least “NGC Catalog” & “Public API” are selected from the “Services Included” dropdown.
3. At the command line: `export NGC_API_KEY=<your-api-key>` to set the API key as a required environment variable.
4. Log in to the NVIDIA NGC docker repo: `echo "$NGC_API_KEY" | docker login nvcr.io --username '$oauthtoken' --password-stdin`
5. Install NGC CLI following instructions here: https://org.ngc.nvidia.com/setup/installers/cli
6. Check the list of available images: `ngc registry image list --format_type csv nvcr.io/nim/*`
7. Get further info for a particular image: `ngc registry image info --format_type ascii nim/meta/llama-3.1-8b-instruct:latest`
8. Run the contents of setup_MPC on the MPC to run the docker image for the `llama-3.1-8b-instruct:latest` NIM.
9. Check connection with:
```
curl -X 'POST' \
    "http://10.167.67.78:8000/v1/completions" \
    -H "accept: application/json" \
    -H "Content-Type: application/json" \
    -d '{"model": "meta/llama3-8b-instruct", "prompt": “Describe Retrieval-Augmented Generation?”, "max_tokens": 64}'
```
