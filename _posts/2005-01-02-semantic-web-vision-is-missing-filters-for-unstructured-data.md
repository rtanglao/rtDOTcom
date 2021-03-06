---
layout: post
title: " Semantic Web vision is missing filters for unstructured data"
created: 1104730531
---
<p>I'd agree that the <a href="http://www.w3.org/People/Berners-Lee/">TBL</a>'s <a href="http://www.w3.org/DesignIssues/Semantic.html">Semantic Web vision</a> is missing filters for unstructured data, but I don't have the solution and I also don't have the answer to Adam's <a href="http://www.adambosworth.net/archives/000038.html">Where Have all the databases gone?</a></p><p>From <a href="http://www.dehora.net/journal/2004/12/let_them_eat_layer_cake_flexibility_versus_clarity_in_data.html">Let them eat layer cake: flexibility versus clarity in data</a>.:</p>
<p><b>QUOTE</b></p><blockquote><p>I'd go so far to argue that this base layer of unstructured data and the layers or services that filter and weed are missing from the Semantic Web stack and that without them it is a non-runner outside the labs, much the same way symbolic AI was until people realized that the more primitive stuff underneath is a feature not a bug.</p>

<p>For RDF, that seems to imply a need for Object Graph Mapping, or Relation Graph Mapping (or both) to integrate RDF graphs with Everything Else and provide domain clarity whenit is needed. Better support is needed for query and storage technology for RDF as keeping domain smarts in queries is a key strategy. Kowari is a good start - it's very much an RDF tool for grownups. I just don't know if it's ready to be imposed on customers yet or can be compared in infrastructure terms to an RDBMS. There's not point in having all that flexibility if your ROI is burnt up on maintenance and knowledge transfer. Even so, there' s nothing out there I know of that addresses concerns about whether we can start working against TBs of RDF short of a fully decentralized P2P query network. I normally dislike generic arguments from scale as they're often a device to close off options rather than think about the problem. In this case however, I think scale is a valid concern.</p>

<p>Another issue will be process. A substantial chunk of software process and architecture is predicated on establishing a domain model. After a decade of pain bringing software testing up front to become a design technique instead of an afterthought, it's not clear we're ready to move domain modelling away from the initial phases. Once you get past the infrastructure side, the thread managers and transaction monitors, all middleware really is, is an articulation of a domain in code. Arguing for some type of dynamically generated middleware or for the death of middleware itself seems dubious if not foolish.</p></blockquote><p><b>UNQUOTE</b></p>



