---
layout: post
title: "ChatGPT and other 'AI' models representational bias: misrepresentation, underrepresentation and overrepresentation; extrinsic harms: representational, performance disparities from 'On the Opportunities and Risks of Foundation Models' (2021) "
---

via Ulrike Hahn's [toot](https://fediscience.org/@UlrikeHahn/110407268640707229)

>@baldur academics, ie non AI vendors, are saying the same things
>though when it comes to LLMs.
>We simultaneously know exactly what they do and don't really...
>that's not just a matter of documentation desire

* The following paper was written in 2021. It's 2023! Have we made any progress since then regarding: "representational bias: misrepresentation, underrepresentation and overreprsentation; extrinsic harms: representational, performance disparities"?
* Here's some juicy quotes from the 161 page paper (plus many pages of references!). Read the whole thing, [On the Opportunities and Risks of Foundation Models (2021)](https://arxiv.org/pdf/2108.07258.pdf) ([overview](https://fsi.stanford.edu/publication/opportunities-and-risks-foundation-models)):

QUOTE

<blockquote>
This report investigates an emerging paradigm for building artificial intelligence (AI) systems
based on a general class of models which we term foundation models. A foundation model is any
model that is trained on broad data (generally using self-supervision at scale) that can be adapted
(e.g., fine-tuned) to a wide range of downstream tasks; current examples include BERT [Devlin et al .
2019], GPT-3 [Brown et al . 2020], and CLIP [Radford et al . 2021]. From a technological point of view,
foundation models are not new — they are based on deep neural networks and self-supervised
learning, both of which have existed for decades. However, the sheer scale and scope of foundation
models from the last few years have stretched our imagination of what is possible; 
</blockquote>

* ...page 131

>**Intrinsic biases**. Properties of the foundation model can lead to harm in downstream systems.
As a result, these intrinsic biases can be measured directly within the foundation model, though
the harm itself is only realized when the foundation model is adapted, and thereafter applied,
i.e., these are latent biases or harms [DeCamp and Lindvall 2020]. We focus on the most widely
studied form of intrinsic bias, **representational bias**, specifically considering **misrepresentation**,
**underrepresentation** and **overrepresentation**. People can be misrepresented by pernicious stereo-
types [Bolukbasi et al . 2016; Caliskan et al . 2017; Abid et al . 2021; Nadeem et al . 2021; Gehman et al .
2020] or negative attitudes [Hutchinson et al . 2020], which can propagate through downstream
models to reinforce this misrepresentation in society [Noble 2018; Benjamin 2019]. People can be
underrepresented or entirely erased, e.g., when LGBTQ+ identity terms [Strengers et al. 2020;
Oliva et al. 2021; Tomasev et al. 2021] or data describing African Americans [Buolamwini and Gebru
2018; Koenecke et al. 2020; Blodgett and O’Connor 2017] is excluded in training data, downstream
models will struggle with similar data at test-time. People can be overrepresented, e.g., BERT
appears to encode an Anglocentric perspective [Zhou et al. 2021a] by default, which can amplify
majority voices and contribute to homogenization of perspectives [Creel and Hellman 2021] or
monoculture [Kleinberg and Raghavan 2021] (§5.6: ethics). **These representational biases pertain to**
**all AI systems, but their significance is greatly heightened in the foundation model paradigm.** Since
the same foundation model serves as the basis for myriad applications, biases in the representation
of people propagate to many applications and settings. Further, since the foundation model does
much of the heavy-lifting (compared to adaptation, which is generally intended to be lightweight),
we anticipate that many of the experienced harms will be significantly determined by the internal
properties of the foundation model.

>**Extrinsic harms**. Users can experience specific harms from the downstream applications that are
created by adapting a foundation model. These harms can be **representational** [Barocas et al. 2017;
Crawford 2017; Blodgett et al . 2020], such as the sexualized depictions of black women produced by
information retrieval systems [Noble 2018], the misgendering of persons by machine translation
systems that default to male pronouns [Schiebinger 2013, 2014], or the generation of pernicious
stereotypes [Nozza et al . 2021; Sheng et al. 2019; Abid et al. 2021]. They can consist of **abuse**, such
as when dialogue agents based on foundation models attack users with toxic content [Dinan et al.
2021; Gehman et al . 2020] or microaggressions [Breitfeller et al . 2019; Jurgens et al . 2019]. All of
these user-facing behaviors can lead to psychological harms or the reinforcement of pernicious
stereotypes [Spencer et al. 2016; Williams 2020].

>In addition to harms experienced by individuals, groups or sub-populations may also be subject
to harms such as **group-level performance disparities**. For example, systems may perform poorly
on text or speech in African American English [Blodgett and O’Connor 2017; Koenecke et al . 2020],
incorrectly detect medical conditions from clinical notes for racial, gender, and insurance-status
minority groups [Zhang et al . 2020b], or fail to detect the faces of people with darker skin tones
[Wilson et al . 2019; Buolamwini and Gebru 2018]. As foundation models are more pervasively
applied, including in high-stakes domains, these disparities can spiral into further, and more severe,
harms. Koenecke et al . [2020] discuss how if African American English speakers cannot reliably
use speech recognition technologies (e.g., due to inequities in underlying foundation models), this
may mean they cannot benefit from certain derivative products (e.g., voice assistants, assistive
technologies) and will be disadvantaged if these technologies are used to conduct interviews for
employment or transcribe courtroom proceedings. More generally, characterizing these group-level
harms (and working towards justice for those harmed) also requires the AI community to improve
its understanding of group-based prejudice [Allport 1954] and social groups: we point to relevant
work in the social sciences and other communities on moving beyond binary treatments of gender.

END QUOTE

### Previously

* April 9, 2023: [Simon Willison: ChatGPT lies. Me: so how can we trust its output to truly be helpful even if we are experts in the domain of discourse? And therefore know how to fact check it?](http://rolandtanglao.com/2023/04/09/p3-simon-wilison-chatgpt-lies-so-how-can-we-trust-it/)
