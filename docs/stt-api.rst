Speech to Text
===================================

You can use the APIs on this page to convert your audio files to text. The conversion process consists of two stages:

    1. Creating a project (`Create API`_)
    2. Query the result and get the text (`Result API`_)


.. _Create API:

Create API
----------

The api you will use to convert your audio file to text.

.. http:post:: https://api.voiser.net/transcription/v1/

**Request Parameters**

    - **userCode -** Your Voiser user code.
    - **projectName -** The name you want to give your project.
    - **fileUrl -** The url of the audio file to be converted to text or the youtube video url.
    - **language -** Language code to be used. (`All Languages`_)
    - **punctuation -** Can be used to set punctuation marks. (`All Options`_)
    - **profanityFilter -** You can hide bad words with the profanity filter. (`All Options`_)

**Response Parameters**

    - **status -** If it returns 1, the record has been created, if it returns 0, a problem has occurred.
    - **message -** Informative message showing the result of your action.
    - **projectCode -** If your project has been successfully created, you can request the `Result API`_ using this project code.



**Example request**:

.. tabs::

    .. code-tab:: php

        $data = array(
            'userCode' => 'YOUR_USER_CODE',
            'projectName' => 'Test Project',
            'fileUrl' => 'https://www.youtube.com/watch?v=0yoaMzhErnA&ab_channel=Voiser',
            'language' => 'en-US',
            'punctuation' => 'DictatedAndAutomatic',
            'profanityFilter' => 'Masked'
        );

        $ch = curl_init('https://api.voiser.net/transcription/v1/');
        curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
        curl_setopt($ch, CURLOPT_HTTPHEADER, array('Content-Type:application/json'));
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
        $response = json_decode(curl_exec($ch));
        curl_close($ch);
        print_r(response);

    .. code-tab:: python

        import requests
        data = {
            'userCode': 'YOUR_USER_CODE',
            'projectName': 'Test Project',
            'fileUrl': 'https://www.youtube.com/watch?v=0yoaMzhErnA&ab_channel=Voiser',
            'language': 'en-US',
            'punctuation': 'DictatedAndAutomatic',
            'profanityFilter': 'Masked'
        }
        response = requests.post('https://api.voiser.net/transcription/v1/', json = data)
        print(response.json())



**Example response**:

.. sourcecode:: json

    {
       "status": "1",
       "message": "Your decryption request has been successfully saved.",
       "projectCode": "ABCDEFGH"
    }



.. _Result API:

Result API
----------

Result API allows you to query the status of the project you have created and, if completed, returns the download urls of the text files.

.. http:post:: https://api.voiser.net/transcription/v1/result

**Request Parameters**

    - **userCode -** Your Voiser user code.
    - **projectCode -** The code of the project you want to query.

**Response Parameters**

    - **status -** If it returns 1, the record has been created, if it returns 0, a problem has occurred.
    - **message -** Informative message showing the result of your action.
    - **result -** It returns urls where you can download txt, srt, xlsx and docx file types.


**Example request**:

.. tabs::

    .. code-tab:: php

        $data = array(
            'userCode' => 'YOUR_USER_CODE',
            'projectCode' => 'ABCDEFGH'
        );

        $ch = curl_init('https://api.voiser.net/transcription/v1/result');
        curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
        curl_setopt($ch, CURLOPT_HTTPHEADER, array('Content-Type:application/json'));
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
        $response = json_decode(curl_exec($ch));
        curl_close($ch);
        print_r(response);

    .. code-tab:: python

        import requests
        data = {
            'userCode': 'YOUR_USER_CODE',
            'projectCode': 'ABCDEFGH'
        }
        response = requests.post('https://api.voiser.net/transcription/v1/result', json = data)
        print(response.json())



**Example response**:

.. sourcecode:: json

    {
       "status": "1",
       "message": "Transcription completed successfully",
       "result": {
            "txt": "TXT_FILE_URL",
            "srt": "SRT_FILE_URL",
            "docx": "DOCX_FILE_URL",
            "xlsx": "XLSX_FILE_URL"
       }
    }


.. _All Languages:

Languages
---------
=================================== =======
Language                            Code
=================================== =======
Afrikaans (South Africa)            af-ZA
Albanian (Albania)                  sq-AL
Amharic (Ethiopia)                  am-ET
Arabic (Algeria)                    ar-DZ
Arabic (Bahrain), (Modern Standard) ar-BH
Arabic (Egypt)                      ar-EG
Arabic (Iraq)                       ar-IQ
Arabic (Israel)                     ar-IL
Arabic (Jordan)                     ar-JO
Arabic (Kuwait)                     ar-KW
Arabic (Lebanon)                    ar-LB
Arabic (Libya)                      ar-LY
Arabic (Morocco)                    ar-MA
Arabic (Oman)                       ar-OM
Arabic (Palestinian)                ar-PS
Arabic (Qatar)                      ar-QA
Arabic (Saudi Arabia)               ar-SA
Arabic (Syria)                      ar-SY
Arabic (Tunisia)                    ar-TN
Arabic (United Arab Emirates)       ar-AE
Arabic (Yemen)                      ar-YE
Armenian (Armenia)                  hy-AM
Azerbaijani (Azerbaijan)            az-AZ
Basque (Spain)                      eu-ES
Bengali (India)                     bn-IN
Bulgarian (Bulgaria)                bg-BG
Burmese (Myanmar)                   my-MM
Catalan (Spain)                     ca-ES
Chinese (Cantonese, Traditional)    zh-HK
Chinese (Mandarin, Simplified)      zh-CN
Chinese (Taiwanese Mandarin)        zh-TW
Croatian (Croatia)                  hr-HR
Czech (Czech Republic)              cs-CZ
Czech (Czech)                       cs-CZ
Danish (Denmark)                    da-DK
Dutch (Belgium)                     nl-BE
Dutch (Netherlands)                 nl-NL
English (Australia)                 en-AU
English (Canada)                    en-CA
English (Ghana)                     en-GH
English (Hong Kong)                 en-HK
English (India)                     en-IN
English (Ireland)                   en-IE
English (Kenya)                     en-KE
English (New Zealand)               en-NZ
English (Nigeria)                   en-NG
English (Philippines)               en-PH
English (Singapore)                 en-SG
English (South Africa)              en-ZA
English (Tanzania)                  en-TZ
English (United Kingdom)            en-GB
English (United States)             en-US
Estonian(Estonia)                   et-EE
Filipino (Philippines)              fil-PH
Finnish (Finland)                   fi-FI
French (Belgium)                    fr-BE
French (Canada)                     fr-CA
French (France)                     fr-FR
French (Switzerland)                fr-CH
Galician (Spain)                    gl-ES
Georgian (Georgia)                  ka-GE
German (Austria)                    de-AT
German (Germany)                    de-DE
German (Switzerland)                de-CH
Greek (Greece)                      el-GR
Gujarati (Indian)                   gu-IN
Hebrew (Israel)                     he-IL
Hindi (India)                       hi-IN
Hungarian (Hungary)                 hu-HU
Icelandic (Iceland)                 is-IS
Indonesian (Indonesia)              id-ID
Irish (Ireland)                     ga-IE
Irish(Ireland)                      ga-IE
Italian (Italy)                     it-IT
Italian (Switzerland)               it-CH
Japanese (Japan)                    ja-JP
Javanese (Indonesia)                jv-ID
Kannada (India)                     kn-IN
Kazakh (Kazakhstan)                 kk-KZ
Khmer (Cambodia)                    km-KH
Korean (Korea)                      ko-KR
Lao (Laos)                          lo-LA
Latvian (Latvia)                    lv-LV
Lithuanian (Lithuania)              lt-LT
Macedonian (North Macedonia)        mk-MK
Malay (Malaysia)                    ms-MY
Maltese (Malta)                     mt-MT
Marathi (India)                     mr-IN
Mongolian (Mongolia)                mn-MN
Nepali (Nepal)                      ne-NP
Norwegian (Bokmål, Norway)          nb-NO
Persian (Iran)                      fa-IR
Polish (Poland)                     pl-PL
Portuguese (Brazil)                 pt-BR
Portuguese (Portugal)               pt-PT
Romanian (Romania)                  ro-RO
Russian (Russia)                    ru-RU
Serbian (Serbia)                    sr-RS
Sinhala (Sri Lanka)                 si-LK
Slovak (Slovakia)                   sk-SK
Slovenian (Slovenia)                sl-SI
Spanish (Argentina)                 es-AR
Spanish (Bolivia)                   es-BO
Spanish (Chile)                     es-CL
Spanish (Colombia)                  es-CO
Spanish (Costa Rica)                es-CR
Spanish (Cuba)                      es-CU
Spanish (Dominican Republic)        es-DO
Spanish (Ecuador)                   es-EC
Spanish (El Salvador)               es-SV
Spanish (Equatorial Guinea)         es-GQ
Spanish (Guatemala)                 es-GT
Spanish (Honduras)                  es-HN
Spanish (Mexico)                    es-MX
Spanish (Nicaragua)                 es-NI
Spanish (Panama)                    es-PA
Spanish (Paraguay)                  es-PY
Spanish (Peru)                      es-PE
Spanish (Puerto Rico)               es-PR
Spanish (Spain)                     es-ES
Spanish (Uruguay)                   es-UY
Spanish (USA)                       es-US
Spanish (Venezuela)                 es-VE
Swahili (Kenya)                     sw-KE
Swahili (Tanzania)                  sw-TZ
Swedish (Sweden)                    sv-SE
Tamil (India)                       ta-IN
Telugu (India)                      te-IN
Thai (Thailand)                     th-TH
Turkish (Turkey)                    tr-TR
Ukrainian (Ukraine)                 uk-UA
Uzbek (Uzbekistan)                  uz-UZ
Vietnamese (Vietnam)                vi-VN
Zulu (South Africa)                 zu-ZA
=================================== =======

.. _All Options:

Punctutation
------------
============================== =======================================
Option                         Description
============================== =======================================
DictatedAndAutomatic (Default) Automatically detects punctuation marks
None                           Does not use punctuation marks
Dictated                       Uses punctuation marks
============================== =======================================

Profanity
------------

============================== =======================================
Option                         Description
============================== =======================================
Masked (Default)               Slang hides words
None                           Slang does not hide words
============================== =======================================