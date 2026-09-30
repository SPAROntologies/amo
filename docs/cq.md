## Competency Questions

AMO can be used for answering several questions related to arguments and how argumentation entities are related to each other.
In the following subsections, some of them are introduced together with their respective SPARQL queries. 

The prefixes that are used in all the SPARQL queries provided below are defined as follows:

    PREFIX amo: <http://purl.org/spar/amo/>
    PREFIX : <http://example.org/>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

### CQ1

What is the claim of a given argument, and which evidence proves it?

    SELECT ?claim ?evidence
    WHERE {
        :argument amo:hasClaim ?claim ;
            amo:hasEvidence ?evidence .
    }

### CQ2

Which warrants lead to a given claim, and which backings attest them?

    SELECT ?warrant ?backing
    WHERE {
        ?warrant amo:leadsTo :consistency-claim .
        OPTIONAL { ?backing amo:backs ?warrant }
    }

### CQ3

What is the degree of force of a given claim, and under which rebuttals is it not valid?

    SELECT ?qualifier ?rebuttal
    WHERE {
        OPTIONAL { ?qualifier amo:forces :consistency-claim }
        OPTIONAL { :consistency-claim amo:isValidUnless ?rebuttal }
    }