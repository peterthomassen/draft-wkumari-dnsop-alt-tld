**Important:** Read CONTRIBUTING.md before submitting feedback or contributing
```




dnsop                                                          W. Kumari
Internet-Draft                                                    Google
Intended status: Informational                               A. Sullivan
Expires: July 20, 2017                                               Dyn
                                                        January 16, 2017


                  The ALT Special Use Top Level Domain
                     draft-ietf-dnsop-alt-tld-07.2

Abstract

   This document reserves a string (ALT) to be used as a TLD label in
   non-DNS contexts, or for names that have no meaning in a global
   context.  It also provides advice and guidance to developers
   developing alternate namespaces.

   [Ed note: Text inside square brackets ([]) is additional background
   information, answers to frequently asked questions, general musings,
   etc.  They will be removed before publication.This document is being
   collaborated on in Github at: https://github.com/wkumari/draft-
   wkumari-dnsop-alt-tld.  The most recent version of the document, open
   issues, etc should all be available here.  The authors (gratefully)
   accept pull requests.  NOTE: This document is currently a parked WG
   document -- as such, all changes are being handled in GitHub and a
   new version will be posted once unparked.

   It had been suggested (off-list) that the draft should contain <TBD>
   instead of .ALT, and then make the WG choose a string before
   publication.  A version of the draft like this was published on
   GitHub (https://github.com/wkumari/draft-wkumari-dnsop-alt-tld/
   tree/7988fcf06100f7a17f21e6993b781690b5774472) and generated no
   feedback.  This version reverts to .ALT at the chairs' request --
   they stated that the document was adopted with the string .alt, it
   has been discussed as .alt, and is more readable as .alt; it would
   also be a difficult consensus call, boiling down to beauty contests.
   If the WG selects a different string ("not-dns" had been suggested in
   the past), the editors will, of course, replace it. ]

   [Ed note: Open question - it is possible that we would need an
   unsecured "delegation" in the root to deal with DNSSEC-- see the
   discussions from .homenet, etc.  Is this a good idea / needed?  It
   seems like part of the larger Special Use Names discussions. ]








Kumari & Sullivan         Expires July 20, 2017                 [Page 1]

Internet-Draft               Reserve ALT TLD                January 2017


Status of This Memo

   This Internet-Draft is submitted in full conformance with the
   provisions of BCP 78 and BCP 79.

   Internet-Drafts are working documents of the Internet Engineering
   Task Force (IETF).  Note that other groups may also distribute
   working documents as Internet-Drafts.  The list of current Internet-
   Drafts is at http://datatracker.ietf.org/drafts/current/.

   Internet-Drafts are draft documents valid for a maximum of six months
   and may be updated, replaced, or obsoleted by other documents at any
   time.  It is inappropriate to use Internet-Drafts as reference
   material or to cite them other than as "work in progress."

   This Internet-Draft will expire on July 20, 2017.

Copyright Notice

   Copyright (c) 2017 IETF Trust and the persons identified as the
   document authors.  All rights reserved.

   This document is subject to BCP 78 and the IETF Trust's Legal
   Provisions Relating to IETF Documents
   (http://trustee.ietf.org/license-info) in effect on the date of
   publication of this document.  Please review these documents
   carefully, as they describe your rights and restrictions with respect
   to this document.  Code Components extracted from this document must
   include Simplified BSD License text as described in Section 4.e of
   the Trust Legal Provisions and are provided without warranty as
   described in the Simplified BSD License.

Table of Contents

   1.  Introduction  . . . . . . . . . . . . . . . . . . . . . . . .   3
     1.1.  Requirements notation . . . . . . . . . . . . . . . . . .   3
     1.2.  Terminology . . . . . . . . . . . . . . . . . . . . . . .   3
   2.  Background  . . . . . . . . . . . . . . . . . . . . . . . . .   3
   3.  The ALT namespace . . . . . . . . . . . . . . . . . . . . . .   4
     3.1.  Choice of the ALT Name  . . . . . . . . . . . . . . . . .   5
   4.  IANA Considerations . . . . . . . . . . . . . . . . . . . . .   5
     4.1.  Domain Name Reservation Considerations  . . . . . . . . .   5
   5.  Security Considerations . . . . . . . . . . . . . . . . . . .   6
   6.  Acknowledgements  . . . . . . . . . . . . . . . . . . . . . .   7
   7.  References  . . . . . . . . . . . . . . . . . . . . . . . . .   7
     7.1.  Normative References  . . . . . . . . . . . . . . . . . .   7
     7.2.  Informative References  . . . . . . . . . . . . . . . . .   8
   Appendix A.  Changes / Author Notes.  . . . . . . . . . . . . . .   8



Kumari & Sullivan         Expires July 20, 2017                 [Page 2]

Internet-Draft               Reserve ALT TLD                January 2017


   Authors' Addresses  . . . . . . . . . . . . . . . . . . . . . . .  10

1.  Introduction

   Many protocols and systems need to name entities.  Names that look
   like DNS names (a series of labels separated with dots) have become
   common, even in systems that are not part of the global DNS
   administered by IANA.

   This document reserves the label "ALT" (short for "Alternate") as a
   Special Use Domain ([RFC6761]).  This label is intended to be used as
   the final (rightmost) label to signify that the name is not rooted in
   the DNS, and that normal registration and lookup rules do not apply.

1.1.  Requirements notation

   The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
   "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this
   document are to be interpreted as described in [RFC2119].

1.2.  Terminology

   This document assumes familiarity with DNS terms and concepts.
   Please see [RFC1034] for background and concepts, and [RFC7719] for
   terminology.  Readers are also expected to be familiar with the
   discussions in [I-D.ietf-dnsop-sutld-ps]

   o  DNS name: Domain names that are intended to be used with DNS
      resolution, either in the global DNS or in some other context

   o  DNS context: The namespace anchored at the globally-unique DNS
      root.  This is the namespace or context that "normal" DNS uses.

   o  non-DNS context: Any other (alternate) namespace.

   o  pseudo-TLD: A label that appears in a fully-qualified domain name
      in the position of a TLD, but which is not registered in the
      global DNS.  This term is in no way intended to be pejorative.

   o  TLD: The last visible label in either a fully-qualified domain
      name or a name that is qualified relative to the root.  See the
      discussion in Section 2.

2.  Background

   The success of the DNS makes it a natural starting point for systems
   that need to name entities in a non-DNS context.




Kumari & Sullivan         Expires July 20, 2017                 [Page 3]

Internet-Draft               Reserve ALT TLD                January 2017


   In many cases, these systems build a DNS-style tree parallel to, but
   separate from, the global DNS.  They often use a pseudo-TLD to cause
   resolution in the alternate namespace, using browser plugins, shims
   in the name resolution process, or simply applications that perform
   special handling of this particular alternate namespace.  An example
   of such a system is the Tor network's [Dingledine2004] use of the
   ".onion" Special-Use Top-Level Domain Name (see [RFC7686]).

   In many cases, the creators of these alternate namespaces have chosen
   a convenient or descriptive string and started using it.  These
   strings are not registered anywhere nor are they part of the DNS.
   However, to users and to some applications they appear to be TLDs;
   and issues may arise if they are looked up in the DNS.

   An alternate name resolution system might be specifically designed to
   provide confidentiality of the looked up name, and to provide a
   distributed and censorship-resistant namespace.  This goal would
   necessarily be defeated if the queries leak into the DNS, because the
   attempt to look up the name would be visible to the operators of root
   name servers at a minimum as well as to any entity viewing the DNS
   lookups going to the root nameservers.

3.  The ALT namespace

   This document reserves the ALT label, using the [RFC6761] process,
   for use as a pseudo-TLD.  This creates an unmanaged sandbox
   namespace.  The ALT label MAY be used in any domain name as a pseudo-
   TLD to signify that this is an alternate (non-DNS) namespace, and
   should not be looked up in a DNS context.

   Alternate namespaces should differentiate themselves from other
   alternate namespaces by choosing a name and using it in the label
   position just before the pseudo-TLD (ALT).  For example, a group
   wishing to create a namespace for Friends Of Olaf might choose the
   string "foo" and use any set of labels under foo.alt.

   As they are in an alternate namespace, they have no significance in
   the regular DNS context and so should not be looked up in the DNS
   context.  Some of these requests will inevitably leak into the DNS
   context (for example, because of clicks on a link in a browser that
   does not have a extension installed that implements the alternate
   namespace resolution), and so the ALT TLD has been added to the
   "Locally Served DNS Zones" ( [RFC6303]) registry to limit how far
   these flow.

   Groups wishing to create new alternate namespaces MAY create their
   alternate namespace under a label that names their namespace under
   the ALT label.  They SHOULD choose a label that they expect to be



Kumari & Sullivan         Expires July 20, 2017                 [Page 4]

Internet-Draft               Reserve ALT TLD                January 2017


   unique and, ideally, descriptive.  There is no IANA controlled
   registry for names under the ALT TLD - it is an unmanaged namespace,
   and developers are responsible for dealing with any collisions that
   may occur under .alt.  Informal lists of namespaces under .alt may
   appear to assist the developer community.

   [Editor note (to be removed before publication): There was
   significant discussion on an IANA registry for the ALT namespace -
   please consult the lists for full thread, but the consensus was that
   it would be better for the IETF / IANA to not administer a registry
   for this.  It is expected one or more unofficial lists will be
   created where people can list the strings that they are using. ]

   Currently deployed projects and protocols that are using pseudo-TLDs
   may choose to move under the ALT TLD, but this is not a requirement.
   Rather, the ALT TLD is being reserved so that current and future
   projects of a similar nature have a designated place to create
   alternate resolution namespaces that will not conflict with the
   regular DNS context.

3.1.  Choice of the ALT Name

   A number of names other than "ALT" were considered and discarded.  In
   order for this technique to be effective the names need to continue
   to follow both the DNS format and conventions (a prime consideration
   for alternate name formats is that they can be entered in places that
   normally take DNS context names); this rules out using suffixes that
   do not follow the usual letter, digit, and hyphen label convention.

4.  IANA Considerations

   The IANA is requested to add the ALT string to the "Special-Use
   Domain Name" registry ([RFC6761], and reference this document.  In
   addition, the "Locally Served DNS Zones" ([RFC6303]) registry should
   be updated to reference this document.

4.1.  Domain Name Reservation Considerations

   This section is to satisfy the requirement in Section 5 of RFC6761.

   The domain "alt.", and any names falling within ".alt.", are special
   in the following ways:

   1.  Human users are expected to know that strings that end in .alt
       behave differently to normal DNS names.  Users are expected to
       have applications running on their machines that intercept
       strings of the form <namespace>.alt and perform special handing
       of them.  If the user tries to resolve a name of the form



Kumari & Sullivan         Expires July 20, 2017                 [Page 5]

Internet-Draft               Reserve ALT TLD                January 2017


       <namespace>.alt without the <namespace> plugin installed, the
       request will leak into the DNS, and receive a negative response.

   2.  Writers of application software that implement a non-DNS
       namespace are expected to intercept names of the form
       <namespace>.alt and perform application specific handing with
       them.  Other applications are not intended to perform any special
       handing.

   3.  In general, writers of name resolution APIs and libraries do not
       need to perform special handing of these names.  If developers of
       other namespaces implement their namespace through a "shim" or
       library, they will need to intercept and perform their own
       handling.

   4.  Caching DNS servers SHOULD recognize these names as special and
       SHOULD NOT, by default, attempt to look up NS records for them,
       or otherwise query authoritative DNS servers in an attempt to
       resolve these names.  Instead, caching DNS servers SHOULD
       generate immediate negative responses for all such queries.

   5.  Authoritative DNS servers SHOULD recognize these names as special
       and SHOULD, by default, generate immediate negative responses for
       all such queries, unless explicitly configured by the
       administrator to give positive answers for private-address
       reverse-mapping names.

   6.  DNS server operators SHOULD be aware that queries for names
       ending in .alt are not DNS names, and were leaked into the DNS
       context (for example, by a missing browser plugin).  This
       information may be useful for support or debugging purposes.

   7.  DNS Registries/Registrars MUST NOT grant requests to register
       "alt" names in the normal way to any person or entity.  These
       "alt" names are defined by protocol specification to be
       nonexistent, and they fall outside the set of names available for
       allocation by registries/registrars.

5.  Security Considerations

   One of the motivations for the creation of the .alt pseudo-TLD is
   that unmanaged labels in the managed root name space are subject to
   unexpected takeover.  This could occur if the manager of the root
   name space decides to delegate the unmanaged label.  Another
   motivation for implementing the .alt namespace to increase user
   privacy for those who do use alternate name resolution systems; it
   would limit how far these queries leak (e.g if used on a system which
   does not implement the alternate resolution system).



Kumari & Sullivan         Expires July 20, 2017                 [Page 6]

Internet-Draft               Reserve ALT TLD                January 2017


   The unmanaged and "registration not required" nature of labels
   beneath .alt provides the opportunity for an attacker to re-use the
   chosen label and thereby possibly compromise applications dependent
   on the special host name.

6.  Acknowledgements

   We would also like to thank Joe Abley, Mark Andrews, Marc Blanchet,
   John Bond, Stephane Bortzmeyer, David Cake, David Conrad, Patrik
   Faltstrom, Olafur Gudmundsson, Paul Hoffman, Joel Jaeggli, Ted Lemon,
   Edward Lewis, George Michaelson, Ed Pascoe, Arturo Servin, and Paul
   Vixie for feedback.

   Christian Grothoff was also very helpful.

7.  References

7.1.  Normative References

   [RFC1034]  Mockapetris, P., "Domain names - concepts and facilities",
              STD 13, RFC 1034, DOI 10.17487/RFC1034, November 1987,
              <http://www.rfc-editor.org/info/rfc1034>.

   [RFC2119]  Bradner, S., "Key words for use in RFCs to Indicate
              Requirement Levels", BCP 14, RFC 2119, DOI 10.17487/
              RFC2119, March 1997,
              <http://www.rfc-editor.org/info/rfc2119>.

   [RFC6303]  Andrews, M., "Locally Served DNS Zones", BCP 163, RFC
              6303, DOI 10.17487/RFC6303, July 2011,
              <http://www.rfc-editor.org/info/rfc6303>.

   [RFC6761]  Cheshire, S. and M. Krochmal, "Special-Use Domain Names",
              RFC 6761, DOI 10.17487/RFC6761, February 2013,
              <http://www.rfc-editor.org/info/rfc6761>.

   [RFC7686]  Appelbaum, J. and A. Muffett, "The ".onion" Special-Use
              Domain Name", RFC 7686, DOI 10.17487/RFC7686, October
              2015, <http://www.rfc-editor.org/info/rfc7686>.

   [RFC7719]  Hoffman, P., Sullivan, A., and K. Fujiwara, "DNS
              Terminology", RFC 7719, DOI 10.17487/RFC7719, December
              2015, <http://www.rfc-editor.org/info/rfc7719>.








Kumari & Sullivan         Expires July 20, 2017                 [Page 7]

Internet-Draft               Reserve ALT TLD                January 2017


7.2.  Informative References

   [Dingledine2004]
              Dingledine, R., Mathewson, N., and P. Syverson, "Tor: The
              Second-Generation Onion Router", , 8 2004,
              <<https://svn.torproject.org/svn/projects/design-paper/
              tor-design.html>>.

   [I-D.ietf-dnsop-sutld-ps]
              Lemon, T., Droms, R., and W. Kumari, "Special-Use Names
              Problem Statement", draft-ietf-dnsop-sutld-ps-00 (work in
              progress), October 2016.

Appendix A.  Changes / Author Notes.

   [RFC Editor: Please remove this section before publication ]

   From -07.1 to -07.2:

   o  Reverted the <TBD> string (at request of chairs).

   o  Added an editors note explaining the above.

   o  Removed some more background, editorializing, etc.

   From -06 to -07.1 (https://github.com/wkumari/draft-wkumari-dnsop-
   alt-tld/tree/7988fcf06100f7a17f21e6993b781690b5774472):

   o  Replaced ALT with <TBD> at the insistence of George.

   From -05 to -06:

   o  Removed a large amount of background - we now have the (adopted)
      tldr document for that.

   o  Made it clear that pseudo-TLD is not intended to be pejorative.

   o  Tried to make it cleat that this is something people can choose to
      use - or not.

   From -04 to -05:

   o  Version bump - we are waiting in the queue for progress on SUN,
      bumping this to keep it alive.

   From -03 to -04:





Kumari & Sullivan         Expires July 20, 2017                 [Page 8]

Internet-Draft               Reserve ALT TLD                January 2017


   o  3 changes - the day, the month and the year (a bump to keep
      alive).

   From -02 to -03:

   o  Incorporate suggestions from Stephane and Paul Hoffman.

   From -01 to -02:

   o  Merged a bunch of changes from Paul Hoffman.  Thanks for sending a
      git pull.

   From -00 to 01:

   o  Removed the "delegated to new style AS112 servers" text -this was
      legacy from the omnicient AS112 days.  (Joe Abley)

   o  Removed the "Advice to implemntors" section.  This used to
      recommend that people used a subdomain of a domain in the DNS.  It
      was pointed out that this breaks things badly if the domain
      expires.

   o  Added text about why we don't want to adminster a registry for
      ALT.

   From Individual-06 to DNSOP-00

   o  Nothing changed, simply renamed draft-wkumari-dnsop-alt-tld to
      draft-ietf-dnsop-alt-tld

   From -05 to -06

   o  Incorporated comments from a number of people, including a number
      of suggestion heard at the IETF meeting in Dallas, and the DNSOP
      Interim meeting in May, 2015.

   o  Removed the "Let's have an (optional) IANA registry for people to
      (opportinistically) register their string, if they want that
      option" stuff.  It was, um, optional....

   From -04 to -05

   o  Went through and made sure that I'd captured the feedback
      received.

   o  Comments from Ed Lewis.





Kumari & Sullivan         Expires July 20, 2017                 [Page 9]

Internet-Draft               Reserve ALT TLD                January 2017


   o  Filled in the "Domain Name Reservation Considerations" section of
      RFC6761.

   o  Removed examples from .Onion.

   From -03 to -04

   o  Incorporated some comments from Paul Hoffman

   From -02 to -03

   o  After discussions with chairs, made this much more generic (not
      purely non-DNS), and some cleanup.

   From -01 to -02

   o  Removed some fluffy wording, tightened up the language some.

   From -00 to -01.

   o  Fixed the abstract.

   o  Recommended that folk root their non-DNS namespace under a DNS
      namespace that they control (Joe Abley)

Authors' Addresses

   Warren Kumari
   Google
   1600 Amphitheatre Parkway
   Mountain View, CA  94043
   US

   Email: warren@kumari.net


   Andrew Sullivan
   Dyn
   150 Dow Street
   Manchester, NH  03101
   US

   Email: asullivan@dyn.com








Kumari & Sullivan         Expires July 20, 2017                [Page 10]
```
