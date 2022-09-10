# 3 kyu - Papers, Please
## Instructions
![Gameplay screencap](https://i.imgur.com/mYgmiOz.jpg)

Papers, Please is an indie video game where the player takes on a the role of a border crossing immigration officer in the fictional dystopian Eastern Bloc-like country of Arstotzka in the year 1982. As the officer, the player must review each immigrant and returning citizen's passports and other supporting paperwork against a list of ever-increasing rules using a number of tools and guides, allowing in only those with the proper paperwork, rejecting those without all proper forms, and at times detaining those with falsified information.
Objective

Your task is to create a constructor function (or class) and a set of instance methods to perform the tasks of the border checkpoint inspection officer. The methods you will need to create are as follow:
Method: receiveBulletin

Each morning you are issued an official bulletin from the Ministry of Admission. This bulletin will provide updates to regulations and procedures and the name of a wanted criminal.

The bulletin is provided in the form of a string. It may include one or more of the following:

    Updates to the list of nations (comma-separated if more than one) whose citizens may enter (begins empty, before the first bulletin):
    ```
    example 1: Allow citizens of Obristan
    example 2: Deny citizens of Kolechia, Republia
    ```
    Updates to required documents
    ```
    example 1: Foreigners require access permit
    example 2: Citizens of Arstotzka require ID card
    example 3: Workers require work pass
    ```
    Updates to required vaccinations
    ```
    example 1: Citizens of Antegria, Republia, Obristan require polio vaccination
    example 2: Entrants no longer require tetanus vaccination
    ```
    Update to a currently wanted criminal
    ```
    example 1: Wanted by the State: Hubert Popovic
    ```
Method: inspect

Each day, a number of entrants line up outside the checkpoint inspection booth to gain passage into Arstotzka. The inspect method will receive an object representing each entrant's set of identifying documents. This object will contain zero or more properties which represent separate documents. Each property will be a string value. These properties may include the following:

    Applies to all entrants:
        passport
        certificate_of_vaccination
    Applies only to citizens of Arstotzka
        ID_card
    Applies only to foreigners:
        access_permit
        work_pass
        grant_of_asylum
        diplomatic_authorization

The inspect method will return a result based on whether the entrant passes or fails inspection:

Conditions for passing inspection

    All required documents are present
    There is no conflicting information across the provided documents
    All documents are current (ie. none have expired) -- a document is considered expired if the expiration date is November 22, 1982 or earlier
    The entrant is not a wanted criminal
    If a certificate_of_vaccination is required and provided, it must list the required vaccination
    A "worker" is a foreigner entrant who has WORK listed as their purpose on their access permit
    If entrant is a foreigner, a grant_of_asylum or diplomatic_authorization are acceptable in lieu of an access_permit. In the case where a diplomatic_authorization is used, it must include Arstotzka as one of the list of nations that can be accessed.

If the entrant passes inspection, the method should return one of the following string values:

    If the entrant is a citizen of Arstotzka: Glory to Arstotzka.
    If the entrant is a foreigner: Cause no trouble.

If the entrant fails the inspection due to expired or missing documents, or their certificate_of_vaccination does not include the necessary vaccinations, return Entry denied: with the reason for denial appended.

Example 1: Entry denied: passport expired.
Example 2: Entry denied: missing required vaccination.
Example 3: Entry denied: missing required access permit.

If the entrant fails the inspection due to mismatching information between documents (causing suspicion of forgery) or if they're a wanted criminal, return Detainment: with the reason for detainment appended.

    If due to information mismatch, include the mismatched item. e.g.Detainment: ID number mismatch.
    If the entrant is a wanted criminal: Detainment: Entrant is a wanted criminal.
    NOTE: One wanted criminal will be specified in each daily bulletin, and must be detained when received for that day only. For example, if an entrant on Day 20 has the same name as a criminal declared on Day 10, they are not to be detained for being a criminal.
    Also, if any of an entrant's identifying documents include the name of that day's wanted criminal (in case of mismatched names across multiple documents), they are assumed to be the wanted criminal.

In some cases, there may be multiple reasons for denying or detaining an entrant. For this exercise, you will only need to provide one reason.

    If the entrant meets the criteria for both entry denial and detainment, priority goes to detaining.
    For example, if they are missing a required document and are also a wanted criminal, then they should be detained instead of turned away.
    In the case where the entrant has mismatching information and is a wanted criminal, detain for being a wanted criminal.

Additional Notes

    Inputs will always be valid.
    There are a total of 7 countries: Arstotzka, Antegria, Impor, Kolechia, Obristan, Republia, and United Federation.
    Not every single possible case has been listed in this Description; use the test feedback to help you handle all cases.
    The concept of this kata is derived from the video game of the same name, but it is not meant to be a direct representation of the game.

If you enjoyed this kata, be sure to check out my other katas.


## Examples
```python

bulletin = """Entrants require passport
Allow citizens of Arstotzka, Obristan"""

inspector = Inspector()
inspector.receive_bulletin(bulletin)

entrant1 = {
    "passport": """ID#: GC07D-FU8AR
    NATION: Arstotzka
    NAME: Guyovich, Russian
    DOB: 1933.11.28
    SEX: M
    ISS: East Grestin
    EXP: 1983.07.10"""
}

inspector.inspect(entrant1) #=> 'Glory to Arstotzka.'
```

## My Solution #1 - 
```python
from datetime import datetime, timedelta

class Inspector:
    def __init__(self):
        self.allow_from = []
        self.deny_from = []
        self.diplo_from = []
        self.nations = ['Arstotzka', 'Antegria', 'Impor', 'Kolechia', 'Obristan', 'Republia', 'United Federation']
        self.req_document = {   'Foreigners':[],
                                'Citizens':[],
                                'Workers':[]}        
        self.req_vaccine = {    'Foreigners':[],
                                'Citizens':[],
                                'Workers':[]}
        self.vac_nation = {'Arstotzka':[], 'Antegria':[], 'Impor':[], 'Kolechia':[], 'Obristan':[], 
                           'Republia':[], 'United Federation':[]}
        self.work_pass = False
        self.native_idcard = False
        
        #self.req_vaccine = {    'polio':[],
        #                        'tetanus':[]}
        self.wanted = []
        self.today = datetime.strptime('1982.11.22','%Y.%m.%d')
        
    
    def receive_bulletin(self, bulletin:str):
        bulls = bulletin.split('\n')
        print('>>> Processing Bulletin')
        for bull in bulls: 
            print(bull)
            if 'Entrants require ' in bull:
                bull = bull.replace('Entrants require ','')
                if ' vaccination' in bull:
                    bull.replace(' vaccination','')
                    shots = bull.split(', ')
                    self.req_vaccine['Foreigners'].extend(shots)
                    print(self.req_vaccine)
                else:
                    docs = bull.split(', ')
                    # Add the required documents to the checklist.
                    for req in self.req_document: self.req_document[req].extend(docs)
                    print(self.req_document)
                
            elif 'Allow citizens of ' in bull:
                bull = bull.replace('Allow citizens of ','')
                countries = bull.split(', ')
                # Add the allowed countries to the checklist.
                for country in countries:
                    if country not in self.allow_from: self.allow_from.append(country)
                    if country in self.deny_from: self.deny_from.remove(country)
                print(self.allow_from)
                
            elif 'Deny citizens of ' in bull:
                bull = bull.replace('Deny citizens of ', '')
                countries = bull.split(', ')
                # Add the banned countries to the checklist.
                for country in countries:
                    if country not in self.deny_from: self.deny_from.append(country)
                    if country in self.allow_from: self.allow_from.remove(country)
                print(self.deny_from)
                
            elif 'Wanted by the State: ' in bull:
                bull = bull.replace('Wanted by the State: ','')
                wanteds = bull.split(', ')
                # Add the wanteds to the wantedlist
                for wanted in wanteds:
                    wanted = wanted.split(' ')
                    self.wanted.append(f'{wanted[1]}, {wanted[0]}')
                print(self.wanted)
                
            elif 'Citizens of Arstotzka require ID card' in bull:
                self.req_document['Citizens'].append('ID_Card')
                self.native_idcard = True
            
            elif 'Foreigners require access permit' in bull:
                self.req_document['Foreigners'].append('access_permit')
                
            elif 'Foreigners require ' in bull:
                bull = bull.replace('Foreigners require ','')
                if ' vaccination' in bull:
                    bull.replace(' vaccination','')
                    shots = bull.split(', ')
                    self.req_vaccine['Foreigners'].extend(shots)
                    print(self.req_vaccine)
                    
            elif 'Citizens of ' in bull:
                bull = bull.replace('Citizens of ','')
                if ' vaccination' in bull:
                    bull = bull.replace(' vaccination', '')
                    if ' no longer require ' in bull:
                        print('BULLSHEIT:',bull)
                        splits = bull.split(' no longer require ')
                        countries, vaccines = splits[0].split(', '), splits[1].split(', ')
                        for country in countries:
                            for vaccine in vaccines: 
                                if vaccine in self.vac_nation[country]: self.vac_nation[country].remove(vaccine)
                    else:
                        splits = bull.split(' require ')
                        countries, vaccines = splits[0].split(', '), splits[1].split(', ')
                        for country in countries: self.vac_nation[country].extend(vaccines)
                    print('vac_nations:', self.vac_nation)
            
            elif 'Workers require work pass' in bull:
                self.work_pass = True
                
            else:
                print(f'WARNING: UNHANDLED BULLETIN - {bull}')
                
        print('>>> Processing Bulletin Complete')
    
    def extract(self, entrant):
        documents = ['passport','certificate_of_vaccination','ID_card',
                     'access_permit','work_pass','grant_of_asylum','diplomatic_authorization']
        
        information = {}
        
        # Check for all available documents.
        for doctype in documents:
            document = entrant.get(doctype, None)
            
            # Extract Data if Document is found on person.
            if document:
                newdoc = {}
                lines = [x.split(': ') for x in document.split('\n')]
                for line in lines:
                    newdoc[line[0]] = line[1]
                
                information[doctype] = newdoc.copy()
                print('Found Document: ', doctype)
                print(newdoc)
                
        return information
    
    
    def inspect(self, entrant):
        information = self.extract(entrant)
        
        
        
        reason = None
        nation = None
        native = False
        foreign = False
        diplom = False
        id_mat = None
        id_name = None
        id_dob = None
        
        
        # Check for detainable offences first.
        for document in information:
            doc = information[document]
            
            # Get ID# if in this document.
            idnumb = doc.get('ID#')
            
            # Store and match to other documents.
            if idnumb:
                if id_mat:
                    if idnumb != id_mat: return 'Detainment: ID number mismatch.'
                else: id_mat = idnumb
            
            # Get nation if it exists in this document.
            nat = doc.get('NATION')
            if nat:
                if nation: 
                    if nat != nation: return 'Detainment: nationality mismatch.'
                else: nation = nat
            
            # Store and match NAME to other documents.
            idname = doc.get('NAME')
            if idname:
                if id_name:
                    if idname != id_name: return 'Detainment: name mismatch.'
                else: id_name = idname
            
            # Store and match DOB to other documents.
            dob = doc.get('DOB')
            if dob:
                if id_dob:
                    if dob != id_dob: return 'Detainment: date of birth mismatch.'
                else: id_dob = dob
            
            # Check if on our wanted list
            if idname:
                if idname in self.wanted: return 'Detainment: Entrant is a wanted criminal.'
            
            # Check if PURPOSE is WORK
            if document == 'access_permit':
                if doc['PURPOSE'] == 'WORK': reason = 'WORK'

        # Run Checks
        if not information.get('passport'): return 'Entry denied: missing required passport.'
        
        # Set all origin flags
        # Check if native.
        if nation == 'Arstotzka': native = True
        else: foreign = True
        if information.get('diplomatic_authorization'): diplom = True
        
        
        
        # Checks across all documents.
        for document in information:
            doc = information[document]
                        
            # Check expiration date.
            expdate = doc.get('EXP')
            if expdate:
                if datetime.strptime(doc['EXP'], '%Y.%m.%d') < self.today: 
                    docname = document.replace('_',' ')
                    return f'Entry denied: {docname} expired.'
            
        # Check if from allowed or banned country.
        if nation:
            if self.allow_from: 
                if nation not in self.allow_from: return f'Entry denied: citizen of banned nation.'
            if self.deny_from:
                if nation in self.deny_from: return f'Entry denied: citizen of banned nation.'
        
        # Check diplomatic access.
        if diplom:
            access = information['diplomatic_authorization']['ACCESS']
            if 'Arstotzka' in access: 
                return 'Cause no trouble.'
            else:
                return 'Entry denied: invalid diplomatic authorization.'
            
        if reason == 'WORK' and self.work_pass:
            if not information.get('work_pass'): return 'Entry denied: missing required work pass.'
        
        # Check foreigners, possible grant of asylum.
        if foreign and self.req_document['Foreigners']:
            for document in self.req_document['Foreigners']:
                if not information.get(document): 
                    if information.get('grant_of_asylum'): continue;
                    docname = document.replace('_',' ')
                    return f'Entry denied: missing required {docname}.'
        
        # If native without ID card.
        if native and self.native_idcard:
            if not information.get('ID_card'): return 'Entry denied: missing required ID card.'
                
        # Check if any nation-related vaccines are required.
        if self.vac_nation[nation]:
            vaccines = information.get('certificate_of_vaccination')
            if vaccines:
                vaccines = vaccines['VACCINES']
                for check in self.vac_nation[nation]:
                    if check not in vaccines:
                        return 'Entry denied: missing required vaccination.'
            else:
                return 'Entry denied: missing required certificate of vaccination.'
                
        # If no objections...
        if nation == 'Arstotzka': return 'Glory to Arstotzka.'
        return 'Cause no trouble.'
```