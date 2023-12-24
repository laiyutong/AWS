<h1>GenAI and image recognition</h1>
<h2>Introduction of AWS services</h2>
<b>Amazon Rekognition</b>: Offers pre-trained and customizable computer vision (CV) capabilities to extract information and insights from your images and videos. With Amazon Rekognition, you can identify objects, people, text, scenes, and activities in images and videos, as well as detect any inappropriate content.<br><br>
<b>Amazon Textract</b>: A machine learning (ML) service that automatically extracts text, handwriting, layout elements, and data from scanned documents. It goes beyond simple optical character recognition (OCR) to identify, understand, and extract specific data from documents.<br><br>
<b>Amazon translate</b>: A neural machine translation service that delivers fast, high-quality, affordable, and customizable language translation.<br><br>
<b>AWS Lambda</b>: A serverless, event-driven compute service that lets you run code for virtually any type of application or backend service without provisioning or managing servers..<br>

<img src="https://i.imgur.com/gWxBGNU.jpg" width="40%">
<img src="https://i.imgur.com/Dsh4UGk.jpg" width="40%">
<img src="https://i.imgur.com/yHShrZ1.png" width="60%">
<img src="https://i.imgur.com/rNokjZx.png" width="60%">
<img src="https://i.imgur.com/wpEw8Io.png" width="60%">
<img src="https://i.imgur.com/rxBbtB7.png" width="60%">
<img src="https://i.imgur.com/uHuxTEg.png" width="60%">
<img src="https://i.imgur.com/HhFa6Jl.png" width="60%">
<img src="https://i.imgur.com/1kKND2n.png" width="60%">
<pre class="text">
import json
import boto3

s3_client = boto3.client('s3')
tt_client = boto3.client('textract')
ts_client = boto3.client('translate')

def lambda_handler(event, context):
    #Change to your own bucket_name and file_name
    bucket_name = "<bucket_name>"
    file_name = "HandsOn1_os.png"
    result = ""
    result_file_name = 'result.txt'
    #Requesting Textract to detect text in the image
    tt_response = tt_client.detect_document_text(
        Document = { 
          'S3Object': {
                'Bucket': bucket_name,
                'Name': file_name
            }
      }
    )
    #Handling the content returned by Textract
    for item in tt_response['Blocks']:
        if item['BlockType'] == 'LINE':
            result += item['Text'] + ' '
    print('\n\n---文字偵測結果---\n' + result)
    #Requesting Translate to translate text
    ts_response = ts_client.translate_text(
        Text = result,
        SourceLanguageCode = 'en',
        TargetLanguageCode = 'zh-TW'
    )
    #Handling the translation result returned by Translate
    result += ts_response['TranslatedText']
    print('\n\n---文字翻譯結果---\n' + ts_response['TranslatedText']) 
    #Saving the results in document format to S3
    s3_client.put_object(
        Body = result,
        Bucket = bucket_name,
        Key = result_file_name,
        ContentType=' text/plain;charset=utf-8'
    )
</pre>
<img src="https://i.imgur.com/lTp0fCq.png" width="60%">
<img src="https://i.imgur.com/xkup43g.png" width="60%">
<img src="https://i.imgur.com/aZqSMLs.png" width="60%">
<img src="https://i.imgur.com/Fzyzhh8.png" width="60%">
<img src="https://i.imgur.com/nEBf6GF.png" width="60%">
<img src="https://i.imgur.com/RGXEPbC.png" width="60%">
<img src="https://i.imgur.com/JSsjv4e.png" width="60%">
<img src="https://i.imgur.com/zCGRAZ0.png" width="60%">
<img src="https://i.imgur.com/nuczKAO.png" width="60%">
<img src="https://i.imgur.com/bUGalPA.png" width="60%">
<img src="https://i.imgur.com/yYByAhH.png" width="60%">
<img src="https://i.imgur.com/rSiCvAq.png" width="60%">
<img src="https://i.imgur.com/9ymCdKM.png" width="60%">
<img src="https://i.imgur.com/xpMBeqA.png" width="60%">
<img src="https://i.imgur.com/6aTNsZl.png" width="60%">
<img src="https://i.imgur.com/hVFqC3f.png" width="60%">
<img src="https://i.imgur.com/OQcHmBG.png" width="60%">
<img src="https://i.imgur.com/lqmLNrp.png" width="60%">
<img src="https://i.imgur.com/lSa6o7L.png" width="60%">
<img src="https://i.imgur.com/lSa6o7L.png" width="60%">
<img src="https://i.imgur.com/IQTXJQt.png" width="60%">
<img src="https://i.imgur.com/A5bpZS2.png" width="60%">
<img src="https://i.imgur.com/PspNcTQ.png" width="60%">
<img src="https://i.imgur.com/LYOXhV7.png" width="60%">
<img src="https://i.imgur.com/efLqqbS.png" width="60%">
<img src="https://i.imgur.com/ckA2FnQ.png" width="60%">
<img src="https://i.imgur.com/ewsHZkX.jpg" width="40%">
<img src="https://i.imgur.com/iK6V4wp.jpg" width="40%">
