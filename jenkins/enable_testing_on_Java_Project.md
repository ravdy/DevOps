# Enable testing on a Java Project

### Pre-requisites
1. Jenkins server on T2.Medium instance
2. Maven setup

Procedure: 
1. Install below plugions
   1. Junit
   2. FindBugs
   3. PMD
   4. CheckStyle
   5. Static Analysis Collector

1. Create a Maven Project
   GitHub URL : https://github.com/ravdy/spring-petclinic.git
   Maven Goals: clean package checkstyle:checkstyle findbugs:findbugs pmd:pmd
   Build settings: chose checkstyle, findbugs, pmd

2. Run you job
