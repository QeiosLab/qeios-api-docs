.. Qeios API documentation master file, created by
   sphinx-quickstart on Fri Dec 27 16:07:00 2019.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Qeios API Documentation
=======================

This documentation aims to explain how to use the REST API that Qeios offers to third-parties.

In order to use the API acting as a Qeios user you need to have an access token. At the moment, the only way to get an access token is by requesting it via email at info@qeios.com.

Usage limits
------------

There is no fixed usage limitation for Qeios REST API and it should not represent a problem for those that use the API in a diligent way. Please contact us (info@qeios.com) if you happen to encounter any limitations that are an obstacle for you.

Reliability
-----------

The API we currently offer is not meant to remain the same, both in format and in functioning. However, we will try our best to make only non-breaking changes. In case of breaking changes, we guarantee that everyone that we know is using the API will be informed in advance.

Qeios is currently a small organization and is still in a transition period. This means that there might be times in which we realize that some standards we've been adopting are not suitable or efficient. In those cases we will make our best to avoid raising problems with third parties while we improve the system.

That being said, we suggest that, at least initially, any third-party software interacting with the API do it in a resilient way. Please do not *just assume* that the API will work or that it will work as intended all the time. As said, we're going to try our best to make it so but for the sake of your clients' experience we are warning you.

Contents
--------

.. toctree::
   :maxdepth: 1

   Authentication <authentication/index>
   Vocabulary <vocabulary/index>
   REST Endpoints <endpoints/index>
