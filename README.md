# Website for GTG

Proof of concept.
Ported over from the [now-defunct GNOME wiki](https://wiki.gnome.org/Apps/GTGa).

## Running locally

While in the main directory in a new terminal session, run:

```sh
docker run --rm -it -v $(pwd):/app -p 4000:4000 ruby:3.3.5 bash
```

Then inside that subshell, run:

```sh
cd app
bundle install
jekyll serve -H 0.0.0.0 --incremental
```

Open [localhost:4000/gtg](http://localhost:4000/gtg) and the website should appear.

