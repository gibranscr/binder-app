# Introduction - Mandy, the Smart Partner

Chemistry is everywhere and manufacturers transform raw materials into final products using knowledge of the chemistry and physical properties of those raw materials. The final products are sold in stores and have chemistry that can work for us or against us. For this reason, it is remarkable to know the ingredients and the chemistry contained in manufactured products. This will allow you to use them more safely and consume them more reliably.

![Alt text](https://github.com/gibranscr/binder-app/blob/main/detergents-350.jpg?raw=True "Mandy")

Chemical compounds exist in different phases at specific temperatures and pressures in given environments. Therefore, it is understood by people or potential consumers that product consumers might be more interested in learning about the correct handling of a product that contains a chemical compound. For example, detergents contain a mixture of chemicals that could change into other harmful chemicals when mixed or stored in stressful environments. As a homemaker, it would be a smart decision to ask Mandy about some of the chemicals that are stored at home. Lotions, creams, makeup, and many other products you buy every day also contain chemicals that you may want to learn more about before you buy.

Mandy uses Wit.ai technology to help identify whether a user wants to mix, store, or search for more information on a chemical compound. PubChem is the world's largest collection of freely accessible chemical information that provides around 100 million records of chemical compounds that are consulted to train Mandy and provide relevant data and information that comes to you in your email. Finally, the reliable data obtained from PubChem is complemented by practical information obtained from the YouTube platform. The result is a text summary of the full video audio and the full audio text of the found video. The query made to YouTube follows the artificial intelligence algorithms used by the platform to offer you the most suitable video to watch. Subsequently, the transcription of the video is sent to the user's email.

The application is divided into three different sections where you can integrate new programming code to make Mandy more complete and useful for potential users. As you will notice, the application contains functions that are directly related to each of these three technologies, so it will be easy for you to identify where you can insert new code or modify the existing one.

The sections are mentioned in the order the application works and these actions start after receiving a question or comment from the user:

    • Implementation of Wit.ai technology
    • PubChem API implementation
    • Implementation of YouTube audio transcription

![Alt text](https://github.com/gibranscr/binder-app/blob/main/workflow-1000-english.jpg?raw=True "Mandy")

## Wit.ai technology Implementation

Mandy - The Smart Companion is an artificial intelligence tool that was programmed in Python that can be used to identify situations in which chemical compounds are involved. Wit.ai is the technology that makes you identify the intention of a user when receiving a question or comment at the beginning of the application.

As you can see, Wit.ai technology identifies when users are interested in doing things that involve knowing about chemical compatibility, storage intent, and information about a chemical compound.

Specifically, the application identifies the following intentions:

    • Intent to search for chemical compatibility: the user wants to know the chemical compatibility of a specific chemical compound. The user will know if it is possible to mix the chemical compounds, and know about the precautions to do so.
    • Storage intent: the user must store a chemical compound or a product that contains a specific chemical compound. The user discovers the storage precautions for these types of chemicals
    • Information search intention: the user wants to know the properties and characteristics of a chemical compound.
    
![Alt text](https://github.com/gibranscr/binder-app/blob/main/mandy-process-1000.jpg?raw=True "Mandy")


### Create a Wit.ai account

You must first create a wit.ai account to obtain an access token for your application. Type wit.ai in any browser with internet access and follow these steps:

     • Open your browser at https://www.wit.ai
     • Click on register (login)
     • Enter an email, username and password
     • Verify the registered email, clicking on the email that Wit.ai will send you.
     • Enter Wit.ai again and click on the button to create a new application (New App)

At the beginning of Mandy's programming code you will find the variable access_token_wit that must contain the token that she generated in her wit.ai account so that she can find this variable at the beginning of the programming code. You will find a code like this:

access_token_wit='XXXXXXXXXXXXXXXXXX'

### Train Mandy with data

Once you have obtained your access token, you can start training your robot to identify the chemical compounds and intentions of the users message. You can train your robot on the wit.ai website manually and custom or use the Wit.ai API provided to automate the training process.

Since you may require hundreds of data to train your robot, you can use the PubChem API in conjunction with the functions that we present below. These functions use excel templates where data was extracted from PubChem and specially modified to enter the data that Wit.ai and Mandy require during the training phase. To learn more about the Wit.ai enpoints consumption procedure, enter the following web address https://wit.ai/docs by clicking on the HTTP API section.

Here you can see how to implement the registration of intents, entities, keywords, etc. to Wit.ai automatically using Excel templates. In essence the programming codes use similar structures that you can implement in python to register your data in Wit.ai. The structure and procedure are as follows:

    • It starts by creating a function which could be called for example: createIntent. This would look like def createIntent ():
    • Identify the endpoint that you are going to use depending on whether you need to register an Intent, Entity, Roles, Keyword, Synonyms or Utterance. You can find them here https://wit.ai/docs and an example of the endpoint to register an Intent is https: / /api.wit.ai/intents
    • Get your access token in Wit.ai as we indicated in the previous section
    • Extract data from your database or Excel file and save it in dictionaries using the Pandas and Python libraries to structure the dictionaries. You must use loops to iterate over the data and form the dictionaries. For example: the final version should give like this for roles (dictionary named data_roles): data_roles = {'roles': roles [i]} and for keywords (dictionary named data_keyword): data_keyword = {'keyword': keyword [ i]}
    • Save structured dictionaries in one as this will be sent to the endpoint address. For example you can create a dictionary called data, like this: data = {** data_roles, ** data_keyword, ** data_synonyms}
    • Structure the headers of the post necessary to send data. This should have your generated wit.ai access token and the indication that you will be working with the json structure. For example: headers = {'authorization': 'Bearer' + wit_access_token, 'Content-Type': 'application / json'}
    • Now it is only to integrate the selected endpoint, your headers formed and the dictionary that you structured with your data to later send all this in a post with the requests library, storing the response obtained from your sending in the variable resp. This would look like this: resp = requests.post (API_ENDPOINT, headers = headers, json = data)
    • So that you can visualize the response obtained from your registry and know if the data was registered correctly, you use the json library with the loads and content attributes. This would look like this if it is saved in the data variable: data = json.loads (resp.content)
    • Finally, it returns the response obtained and stored in data outside the function, this is done by including the command: return data as the final line.

This procedure is repeated in a similar way similar to either the Entities, Roles, Keywords, Synonyms or Utterances that you want to register to train Mandy. This would send N number of data or in other words N number of questions, comments or user requests in your Wit.ai account for a better Mandy training.

You can compare and learn about the similarities and differences of the programming codes needed to post data on Wit.ai with the standard approach that we just mentioned. Remember that the most complicated endpoint you can structure is the Utterances. The others are simpler and easier to structure in your programming code.

The programming codes that we will present below do not have the code fragments where the data is extracted from excel. These files and complete codes can be downloaded here https://github.com/gibranscr/binder/tree/master, it is only that you delete the lines of code that have the # sign to be considered as active code. The lines can be identified with the following codes:

#usando plantilla de excel 
#data_excel=pd.read_excel('wit-training-model.xlsx')
#data_table=pd.DataFrame(dataexcel,columns['Intent','Entity','Keywords','Synonym_1','Synonym_2','Synonym_3','Synonym_4','PubChem_CID'])


#usando plantilla de excel
#data_roles=data_table.iloc[i]['roles']
#data_keyword=data_table.iloc[i]['Keywords']
#data_synonyms=data_table.iloc[i]['Synonym_1']
#data_entity=data_table.iloc[i]['Entity']
#API_ENDPOINT='https://api.wit.ai/entities/'+data_entity+'/keywords?v=20200624'

Remember that when activating these lines you would have to erase the lines where the same variables are defined for the correct operation of the programming algorithm.


#### Intents - API programming code

Below, you can see the programming code for Intents training in wit.ai for Mandy.

import requests
import json
import pandas as pd


API_ENDPOINT='https://api.wit.ai/intents'
wit_access_token='FE5AVTCKI4WL7X2S4RCZPS4L7D53S5QP'
def createIntent():
    #usando plantilla de excel
    #data=pd.read_excel('wit-training-model.xlsx')
    #intents=data=pd.DataFrame(data,columns=['Intent',Entity','Keywords','Synonym_1','Synonym_2','Synonym_3','Synonym_4','PubChem_CID'])
    
    intents=['info_storage_compatibility','get_ghs_classification','confirm_storage_compatibility']
    
    for i in range(len(intents)):
        dat={'name':intents[i]}
        
        #usando plantilla de excel
        #intents.iloc[i]['Intent']

        headers = {'authorization': 'Bearer ' + wit_access_token,'Content-Type': 'application/json'}
        resp=requests.post(API_ENDPOINT,headers=headers,json=dat)
        data=json.loads(resp.content)
        print(data)
    return data
if __name__ == '__main__':
    textt=createIntent()
    if textt is None:
        print("\n Result: Intent Saved on Wit.ai Success (200){}")

#### Entities - API programming code


Below you will see the programming code for Entities training in wit.ai for Mandy.

import requests
import json
import pandas as pd

API_ENDPOINT='https://api.wit.ai/entities/chemical_substance/keywords?v=20200624'
wit_access_token='FE5AVTCKI4WL7X2S4RCZPS4L7D53S5QP'

def createKeyword():
    #data_excel=pd.read_excel('wit-training-model.xlsx')
    #data_table=pd.DataFrame(dataexcel,columns=['Intent','Entity','Keywords','Synonym_1','Synonym_2','Synonym_3','Synonym_4','PubChem_CID'])
    
    #241-313
    #choose one entity and add n keywords with n synonyms per keyword created
    entities=['chemical_substance']
    keyword=['Hydrochloric Acid']
    synonyms=[['Acid, Hydrochloric','Acid, Muriatic','Hydrogen Chloride','Chloride, Hydrogen','Hydrochloric Acid']]
    
    #roles=[['hazard_good_spec'],['storage_substance','mixture_compound'],['chemical_characteristic'],['fluid_state']]

    for i in range(len(keyword)):
        #usando plantilla de excel
        #data_roles=data_table.iloc[i]['roles']
        #data_keyword=data_table.iloc[i]['Keywords']
        #data_synonyms=data_table.iloc[i]['Synonym_1']
        #data_entity=data_table.iloc[i]['Entity']
        #API_ENDPOINT='https://api.wit.ai/entities/'+data_entity+'/keywords?v=20200624'
        
        
        data_roles={'roles':roles[i]}
        data_keyword={'keyword':keyword[i]}
        data_synonyms={'synonyms':synonyms[i]}
        data={**data_roles,**data_keyword,**data_synonyms}

        #dat={'name':'chemical_substance','roles':['storage_substance','mixture_compound']}
        #dat={'name':'get_storage_compatibility','roles':['class_of_substance']}
        #print(newintent)
        headers = {'authorization': 'Bearer ' + wit_access_token,'Content-Type': 'application/json'}
        resp=requests.post(API_ENDPOINT,headers=headers,json=data)
        data=json.loads(resp.content)
        print(data)
    return data
if __name__ == '__main__':
    #intent=input()
    textt=createKeyword()
    if textt is None:
        print("\n Result: Intent Saved on Wit.ai Success (200){}")

#### Utterances - API programming code

Below you will see the programming code for the training of statements (Utterances) in wit.ai for Mandy.

import requests
import json
import pandas as pd


API_ENDPOINT='https://api.wit.ai/intents'
wit_access_token='FE5AVTCKI4WL7X2S4RCZPS4L7D53S5QP'
def createIntent():
    #usando plantilla de excel
    #data=pd.read_excel('wit-training-model.xlsx')
    #intents=data=pd.DataFrame(data,columns=['Intent',Entity','Keywords','Synonym_1','Synonym_2','Synonym_3','Synonym_4','PubChem_CID'])
    
    intents=['info_storage_compatibility','get_ghs_classification','confirm_storage_compatibility']
    
    for i in range(len(intents)):
        dat={'name':intents[i]}
        
        #usando plantilla de excel
        #intents.iloc[i]['Intent']

        headers = {'authorization': 'Bearer ' + wit_access_token,'Content-Type': 'application/json'}
        resp=requests.post(API_ENDPOINT,headers=headers,json=dat)
        data=json.loads(resp.content)
        print(data)
    return data
if __name__ == '__main__':
    textt=createIntent()
    if textt is None:
        print("\n Result: Intent Saved on Wit.ai Success (200){}")

It is important that you identify the moment when Mandy shows you the identified chemical compounds and the identified intention. You get this data with the main function called Wit_request that we present to you in the next section. Subsequently, these data will be used to continue with the sending of relevant information and transcription of the audio of videos found on YouTube.

### Identification of Chemical Compounds and Intentions

![Alt text](https://github.com/gibranscr/binder-app/blob/main/label-detergent-small.jpg?raw=True "Mandy")

The application uses the following Python libraries that allow it to get the correct information for the user:

     • Wit: this library identifies the user's intent when something is mentioned in the application input box
     • json: this library is used to handle the data received from the response of the different APIs built into the application.

This section contains a main function called wit_request that receives the question from the user and the token that was generated in wit.ai. Depth, extract, and json_extract are two sub-functions that are used to extract the data received from wit.ai so that it only gets the names of the chemicals and the intent of the user message.

#### Wit_request Main Function

def wit_request(question,access_token_wit):
    
    client = Wit(access_token=access_token_wit)
    resp=client.message(msg=question)

    data_extraction=json.dumps(resp)
    data=json.loads(data_extraction)

    def depth(data):
        if "entities" in data:
            return 1 +  max([0] + list(map(depth, data['entities'])))      
        else:
            return 1
    levels_with_entities=depth(data)
    
    def json_extract(obj,key):
        arr=[]
        def extract(obj,arr,key):
            if isinstance(obj,dict):
                for k,v in obj.items():
                    if isinstance(v,(dict,list)):
                        extract(v,arr,key)
                    elif v==key:
                        if obj not in arr:
                            arr.append(obj)
            elif isinstance(obj,list):
                for item in obj:
                    extract(item,arr,key)
            return (arr)
        values=extract(obj,arr,key)
        return values
    #get intents
    intent=resp['intents'][0]['name']
    #extract chemicals that wit.ai found
    result_confirm=json_extract(data,'chemical_substance')
    chemicals=[]
    number_chemicals=len(result_confirm)
    for q in range(number_chemicals):
        chemicals.append(result_confirm[q]['value'])   
    
    return (chemicals,intent)

#### Json_Extract and Extract Subfunctions

These functions are used to obtain the names and intents of the chemicals from the wit.ai response that is stored in the data variable. Essentially, these functions receive an object that can be a list, array, or dictionary and parse the data from those objects until the values ​​of the key intents and the key of chemical_subtance are reached after iterating over the different objects contained in the json response. The functions are integrated into the main function called Wit_request. These sub-functions use the concept of a recursive function, which allows you to explore through the different levels in your json structure.

Specifically, the extract function uses recursive functions, so we suggest you identify the following:

    • How many levels are there in your json structure?
    • Where does a dictionary start and end, a list?
    • Does your dictionary key have a built-in dictionary?
    • Does the value of your dictionary have a built-in dictionary or list, which would represent you considering going one more level to extract the required data?
    • Is your key or value letters or numbers?
    • Remember that you can use empty lists to save the data found as in the case of the list created arr

Taking these considerations and visualizing the response of wit.ai (data variable) you will be able to better understand the extract function and the concept of recursive functions that we present below:

        def extract(obj,arr,key):
            if isinstance(obj,dict):
                for k,v in obj.items():
                    if isinstance(v,(dict,list)):
                        extract(v,arr,key)
                    elif v==key:
                        if obj not in arr:
                            arr.append(obj)
            elif isinstance(obj,list):
                for item in obj:
                    extract(item,arr,key)
            return (arr)
        values=extract(obj,arr,key)
        return values


Also, we suggest you read a little more about recursive functions in python so that you can extract the proper data in wit.ai and in the PubChem library.

The end result of the tutorial is that Mandy is trained in such a way that the chemical compounds and the intention of using them are correctly identified. Later you will be able to continue with the integration of the second phase of the application where you will be able to learn about the safety procedures for the use of the identified chemicals and learn better about their advantages, disadvantages and ways of obtaining an adequate availability of these. The PubChem and Youtube technologies integrated into Mandy's application can be found in the full tutorial by downloading it here https://github.com/gibranscr/binder/tree/master.

We hope that this tutorial has been to your liking, so we invite you to learn about wit.ai and other technologies that you may be using in your daily activities with a little programming on your part. Good time and until next time.
