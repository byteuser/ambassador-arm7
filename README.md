# ambassador-arm7
This docker image is a mashup of [ctlc/ambassador](https://github.com/CenturyLinkLabs/ctlc-docker-ambassador) and [suutari/ambassador](https://github.com/suutari/docker-ambassador). 
Also, note that we are NOT claiming that this old-school ambassador pattern is the best way to go today. It's simply one way to do things.

## Usage

The "[Link via an ambassador container](https://docs.docker.com/articles/ambassador_pattern_linking/)" article on the Docker website explains the ambassador pattern and potential usage quite clearly. Just replace `svendowideit/ambassador` with `openstf/ambassador` where required.

## Caveats

If the internal `socat` somehow manages to die, it won't get restarted. Instead, the container dies with it. We recommend using a proper [systemd Service unit](http://www.freedesktop.org/software/systemd/man/systemd.service.html) for automatically restarting it.

However, if your ambassador handles more than one link, then even if all links except one die, the ambassador will happily stay alive waiting for the last link to die too, which means that systemd won't notice a thing and has no chance to restart the unit to reopen sockets. Most if not all traditional ambassador pattern implementations suffer from this problem as well, many of them even if you're only using a single link.

## License

See [LICENSE](LICENSE).

Copyright © Simo Kinnunen. All Rights Reserved.
