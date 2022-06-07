## Purpose

This deployment guide is developed based on outcomes of GovTech’s Capability Centre for Government ICT infrastructure (CapCEN) Proof of Concept (POC) for Cloud Resource Transformation Solution (CRTS) that was targeted for Amazon Web Services (AWS) in Government on Commercial  Cloud (GCC)1.0. It consists of detailed resources required, tools utilized and steps necessary for deployment of this solution into agencies’ AWS environment in GCC1.0.

## Audience

The intended audience are:
<ol type="a">
  <li>Infrastructure Engineers</li>
  <li>DevOps Engineers</li>
</ol>

## Terms and Acronyms

{% assign terms = data.acronyms | where_exp: "item" %}

{% for item in acronyms %}
 <details>
  <summary>{{ item.term }}</summary>
   <p>{{ item.acronym1 }}</p>
   
   {% if item.acronym2 == nil %}
     <p>{{ item.acronym2 }}</p>
   {% endif %}

   {% if item.acronym3 == nil %}
     <p>{{ item.acronym3 }}</p>
   {% endif %}
   
 </details>
{% endfor %}