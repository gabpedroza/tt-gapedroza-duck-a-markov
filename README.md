![](../../workflows/gds/badge.svg) ![](../../workflows/docs/badge.svg) ![](../../workflows/test/badge.svg) ![](../../workflows/fpga/badge.svg)

# Duck-a-markov

A reverse, (almost) deterministic whack-a-mole game! You are a worm which must duck from a duck! The duck starts with a random view of the movement pattern of the worm, but as it watches you, learns from you! 

(Concretely, it maintains a look up table of two movements, the entries of which are its prediction of your next move after them. The look up table is indexed by whether move t was even or odd, and by the exact move t+1; then it predicts movement t+2).

The fact that the duck behaves deterministically (after its 2nd order Markov model of you has been filled) means it is technically possible to beat it forever! Can you do it?

## Run it

1. Keys 0 to 3 select the dirt patch the worm appears in.
2. Screen flashes red when you are caught. Then the grass colour changes to indicate how many times you have been hit. After 4 hits, it resets the colour (i.e. you lost), but the duck doesn't forget you.

## Files

- `src/duck_a_markov.v`: the game itself: you are a worm which must dodge a duck.
- `src/hvsync_generator.v`: makes the VGA timing (640 x 480 at 60 Hz). It is provided for you, so you do not need to write or change it. This is written by Vulkos it seems.

The design drives `uo_out` in the TinyVGA PMOD order, {hsync, B0, G0, R0, vsync, B1, G1, R1}, with two bits per colour.

The flow was set up by Vulkos (including a bit of this README). The code was based off their racing game but obviously heavily modified. I used some help of LLMs specially to ideate some area reductions and come up with LFSR PRNGs. The bulk of the code was written by me rushiedly; you can tell because of its jankiness.

---

Below is the tiny tapeout readme that came with the Vulkos flow.

# Tiny Tapeout Verilog Project Template

- [Read the documentation for project](docs/info.md)

## What is Tiny Tapeout?

Tiny Tapeout is an educational project that aims to make it easier and cheaper than ever to get your digital and analog designs manufactured on a real chip.

To learn more and get started, visit https://tinytapeout.com.

## Set up your Verilog project

1. Add your Verilog files to the `src` folder.
2. Edit the [info.yaml](info.yaml) and update information about your project, paying special attention to the `source_files` and `top_module` properties. If you are upgrading an existing Tiny Tapeout project, check out our [online info.yaml migration tool](https://tinytapeout.github.io/tt-yaml-upgrade-tool/).
3. Edit [docs/info.md](docs/info.md) and add a description of your project.
4. Adapt the testbench to your design. See [test/README.md](test/README.md) for more information.

The GitHub action will automatically build the ASIC files using [LibreLane](https://www.zerotoasiccourse.com/terminology/librelane/).

## Enable GitHub actions to build the results page

- [Enabling GitHub Pages](https://tinytapeout.com/faq/#my-github-action-is-failing-on-the-pages-part)

## Resources

- [FAQ](https://tinytapeout.com/faq/)
- [Digital design lessons](https://tinytapeout.com/digital_design/)
- [Learn how semiconductors work](https://tinytapeout.com/siliwiz/)
- [Join the community](https://tinytapeout.com/discord)
- [Build your design locally](https://www.tinytapeout.com/guides/local-hardening/)

## What next?

- [Submit your design to the next shuttle](https://app.tinytapeout.com/).
- Edit [this README](README.md) and explain your design, how it works, and how to test it.
- Share your project on your social network of choice:
  - LinkedIn [#tinytapeout](https://www.linkedin.com/search/results/content/?keywords=%23tinytapeout) [@TinyTapeout](https://www.linkedin.com/company/100708654/)
  - Mastodon [#tinytapeout](https://chaos.social/tags/tinytapeout) [@matthewvenn](https://chaos.social/@matthewvenn)
  - X (formerly Twitter) [#tinytapeout](https://twitter.com/hashtag/tinytapeout) [@tinytapeout](https://twitter.com/tinytapeout)
  - Bluesky [@tinytapeout.com](https://bsky.app/profile/tinytapeout.com)
