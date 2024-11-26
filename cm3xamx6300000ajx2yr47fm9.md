---
title: "SAA - C03 Certification: Machine Learning"
datePublished: Mon Nov 25 2024 17:20:06 GMT+0000 (Coordinated Universal Time)
cuid: cm3xamx6300000ajx2yr47fm9
slug: saa-c03-certification-machine-learning
tags: aws

---

## Amazon Rekognition

* Find objects, text, people, and scenes in images and videos using ML
    
* Facial analysis and facial search to do user verification, people counting
    
* Create a database of “familiar faces” or compare them to celebrities
    

> Use cases:
> 
> * Labeling
>     
> * Content Moderation
>     
> * Text Detection
>     
> * Face Detection and Analysis
>     
> * Face Search and Verification
>     
> * Celebrity Regonnition
>     
> * Pathing
>     

### Content Moderation

* Detect content that is inappropriate, unwanted, or offensive (images and videos)
    
* Used in social media, broadcast media, advertising, and e-commerce situations to create a safer user experience
    
* Set a minimum confidence Threshold for items that will be flagged
    

## Amazon Transcribe

* Automatically convert speech to text
    
* **Use cases:**
    
    * transcribe customer service calls
        
    * automate closed captioning and subtitling
        
    * generate metadata for media assets
        

## Amazon Polly

* Turn text into lifelike speech using deep learning
    
* Allowing the creation application to talk
    

### Lexicon & SSML

* Customize the pronunciation of words with **Pronunciation Lexicons**
    
    * Stylized words: St3ph4ne =&gt; “Stephane”
        
    * Acronyms: AWS =&gt; “Amazon Web Services”
        
* Upload the lexicons and use them in **SynthesizeSpeech**
    
* Generate speech from plain text or documents marked up with **Speech Synthesis Markup Language (SSML)**
    

## Amazon Lex & Connect

* Amazon Lex: (like Siri)
    
    * Automatic Speech Recognition to convert speech to text
        
    * Natural Language Understanding to recognize the intent of text, callers
        
    * Help build chatbots, call center bots
        
* Amazon Connect:
    
    * Receive calls, create contact flows, and cloud-based virtual contact center
        
    * Can integrate with other CRM systems or AWS
        
    * No upfront payments, 80% cheaper than traditional contact center solutions
        

## Amazon Comprehend

* For NLP
    
* Fully managed and serverless service
    
* Uses ML to find insights and relationships in text
    
* Use cases:
    
    * analyze customer interactions
        
    * create and group articles by topics
        

## Comprehend Medical

* Detects and returns useful information in unstructured clinical text: Physician’s notes, Discharge summaries, and Test results,…
    
* Use NLP to detect Protected Health Information
    

## SageMaker

* Fully managed service to build LM models
    
* Typically difficult to do all the processes in one place + provision services
    

## Amazon Forecast

* Fully managed service that uses ML to deliver highly accurate forecasts
    
* Example: predict the future sales of a raincoat
    
* Use cases: Product Demand Planning, Financial Planning,…
    

## Amazon Kendra

* Fully managed document search service powered by ML
    
* Extract answers from a document
    

## Amazon Personalize

* Fully managed ML service to build apps with real-time personalized recommendations
    
* Use cases: retail stores, media, and entertainment,…
    

## Amazon Textract

* Automatically extracts text, handwriting, and data from any scanned documents using AL and ML
    

## Summary

* Rekognition: face detection, labeling
    
* Transcribe: audio to text
    
* Polly: text to audio
    
* Translate: translations
    
* Lex: build conversational bots- chatbots
    
* Connect: cloud contact center
    
* Comprehend: NLP
    
* SageMaker: build ML model
    
* Forecast: build highly accurate forecasts
    
* Kendra: ML-powered search engine
    
* Personalize: real-time personalized recommendations
    
* Textract: detect text and data in documents