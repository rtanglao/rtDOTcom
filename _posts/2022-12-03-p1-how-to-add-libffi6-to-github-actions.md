---
layout: post
title: "How To: Make libffi6 work with Github actions and Ubuntu 22.04 and Ubuntu 20.04"
---
* [A few days ago](https://github.com/rtanglao/rt-kits-api3/actions/runs/3584193643/jobs/6030554003) my Github Action for rt-kits-api3 broke because the default operating system for `ubuntu-latest` changed to `22.04.1` from `18.04`
* The easy way to fix this was to change `ubuntu-latest` to `ubuntu-18.04` but that will break in April 2023.
* The proper way to fix it for now until the ruby `ffi` gem is fixed to work with `libffi7` is to install `libffi6` (alongside 7l; `libffi6` is not part of Ubuntu 22.04 and 20.04 by default) manually using the following yaml in the [Github Actions file](https://github.com/rtanglao/rt-kits-api3/blob/main/.github/workflows/getffquestions.yml):

```yaml
- name: Install libffi6
      run: |-
        curl -LO http://archive.ubuntu.com/ubuntu/pool/main/libf/libffi/libffi6_3.2.1-8_amd64.deb
        sudo dpkg -i libffi6_3.2.1-8_amd64.deb
```
* There has to  be a better way :-) but I couldn't find one! Maybe upgrading to Ruby 3.x from 2.7.x would fix it?
* For full details, see: [fix libffi7 issue before March 2023 when ubuntu 18.04 is deprecated #2](https://github.com/rtanglao/rt-kits-api3/issues/2#top)  

### Previously

* March 13, 2022: [Free  computing e.g. at github actions isn't free; free cloud computing  considered harmful (because environment: see  Steven Gonzalez Monserrate  January 27, 2022: The Cloud Is Material: On the Environmental Impacts  of Computation and Data Storage via The Staggering Ecological Impacts of  Computation and the Cloud via Kottke](http://rolandtanglao.com/2022/03/13/p1-free-computing-considered-harmful-band-for-environment/)        
* March 14, 2021:  [On  March 3, 2021 Github action in rt-kits-api3 to get Firefox support  questions broke because ruby gem ffi-1.13.1 wasn't found, fix:change  Gemfile ffi version to 1.15.0](http://rolandtanglao.com/2021/03/14/p1-github-actions-broke-ruby-dependency-no-local-debugging/)        
* October 18, 2020: [Github Actions are super powerful and yaml is super confusing](http://rolandtanglao.com/2020/10/18/p1-github-actions-super-great-yaml-is-super-confusing/)        
