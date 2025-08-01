# macondo

A crossword board game solver. It may be the best one in the world (so far).

Current master build status:

![Build status](https://github.com/domino14/macondo/actions/workflows/build-and-deploy-bot.yml/badge.svg)

# What is a crossword board game?

A crossword board game is a board game where you take turns creating crosswords
with one or more players. Some examples are:

- Scrabble™️ Brand Crossword Game
- Words with Friends
- Lexulous
- Yahoo! Literati (defunct)

# How to use Macondo:

See the manual and information here:

https://domino14.github.io/macondo

# protoc

To generate pb files, run this in the macondo directory:

`go generate`

Make sure you have done

`go install google.golang.org/protobuf/cmd/protoc-gen-go@latest`

# Creating a new release

(Notes mostly for myself)

Tag the release; i.e. `git tag vX.Y.Z`, then `git push --tags`. This will kick off a github action that builds and uploads the latest binaries. Then you should generate some release notes manually.

# Using Triton

If you want to use the neural network model, I recommend you use Triton server
rather than the default Go server. It's _much_ faster, but it's not trivial to run locally.

If your macondo directory is at `$HOME/code/macondo` you would run `docker run` with these parameters:

```
docker run --gpus all --rm -p 8000:8000 -p 8001:8001 -p 8002:8002     -v $HOME/code/macondo/data/strategy/default/models/:/models     nvcr.io/nvidia/tritonserver:25.06-py3     tritonserver --model-repository=/models
```

You may need to install the NVIDIA Container Toolkit to use your GPU for inference.

Then you can run Macondo with the `MACONDO_TRITON_USE_TRITON` environment variable set to `true`.

### Attributions

Wolges-awsm is Copyright (C) 2020-2022 Andy Kurnia and released under the MIT license. It can be found at https://github.com/andy-k/wolges-awsm/. Macondo interfaces with it as a server.

KLV and KWG are Andy Kurnia's leave and word graph formats. They are small and fast! See more info at https://github.com/andy-k/wolges

Some of the code for the endgame solver was influenced by the MIT-licensed Chess solver Blunder. See code at https://github.com/algerbrex/blunder
