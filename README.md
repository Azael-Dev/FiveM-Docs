Azael - FiveM Documentation
===================

Source of [docs.azael.dev][docs] for [fivem.azael.dev][azael].

Development
-----------

Install [Hugo][gohugo], then run:

```sh
git submodule update --init --recursive
hugo server -D
```

Checking for dead links
-----------------------

Install [Wget][wget], start a Hugo server, then run:

```sh
wget --spider -o ./wget.log -e robots=off -w 1 -r -p http://localhost:1313
```

More info on that [here][check-dead-links].

[azael]: https://fivem.azael.dev
[docs]: https://docs.azael.dev
[gohugo]: https://gohugo.io
[wget]: http://www.gnu.org/software/wget/
[check-dead-links]: http://n390.com/blog/find-broken-links-using-wget
