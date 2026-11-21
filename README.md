<img src="assets/logo.png" width="112" height="112" alt="RankBand logo">

# RankBand

Look up the finite interval represented by a histogram bin. This Blyx library is part of the numerics and visualization collection.

Histogram counts identify the bucket containing a percentile, not its exact location. Return the interval before deciding whether a threshold was breached. [Prometheus, histogram quantiles](https://prometheus.io/docs/practices/histograms/)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-rankband.git
cd blyx-rankband
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-rankband) · [Package page](https://www.blyx-lang.space/packages/rankband) · [Handbook](https://doc.blyx-lang.space/guide/nightingale)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-rankband.git vendor/rankband
```

```blyx
use vendor::rankband::rankband;

fn main() {
    let edges = [0, 10, 30];
    let index = 1.0;
    let result = rankband_interval(edges, index);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
10
30
20
```

## API

`rankband_interval(edges, index)`

Edges must be strictly increasing. Returns [lower edge, upper edge, span]. Bins are half-open except the last, which may include its upper edge. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| edges | Vector of values, each a finite number |
| index | A nonnegative exact integer |

## In use

[Nightingale](https://github.com/Rahulchaube1/blyx-nightingale) uses this module to bound a percentile from histogram counts without inventing a within-bin value.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-rankband/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). The package artwork uses [Lucide icons](https://lucide.dev/license); see [artwork notices](assets/NOTICE.txt).

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
