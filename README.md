# intership_task1

Objective: Clean and prepare a raw dataset (with nulls, duplicates, inconsistent formats).
Tools: Excel / Python (Pandas)
Deliverables: Cleaned dataset + short summary of changes

Dataset names from Kaggle:
                          Medical Appointment No Shows
import pandas as pd
mapp=pd.read_csv('KaggleV2-May-2016.csv')
mapp
1: Identify and handle missing values using .isnull() in Python or filters in Excel.
   mapp.isnull().sum()
   
2: Remove duplicate rows using .drop_duplicates() or Excel’s “Remove Duplicates”.
   m_dups = mapp[mapp.duplicated]
   print (len(m_dups))
   mapp2 = mapp.drop(columns=['AppointmentID'])
   print("Duplicates across fields:", mapp2.duplicated().sum())
   mapp_unique = mapp2.drop_duplicates
   
3: Standardize text values like gender, country names, etc.
     mapp['Gender']= (mapp['Gender'].str.upper().replace({"F": "Female","M": "Male"}))
     mapp
     
4: Convert date formats to a consistent type (e.g., dd-mm-yyyy).
      mapp['ScheduledDay'] = pd.to_datetime(mapp['ScheduledDay']).dt.strftime('%d-%m-%Y')
      mapp['AppointmentDay'] = pd.to_datetime(mapp['AppointmentDay']).dt.strftime('%d-%m-%Y')
      mapp
      
5: Rename column headers to be clean and uniform (e.g., lowercase, no spaces).
    mapp=mapp.rename(columns={'PatientId':'Patient_id','AppointmentID':'Appointment_id','ScheduledDay':'Scheduled_date',
                         'AppointmentDay':'Appointment_date','Hipertension':'Hypertension','Handcap':'Handicap','SMS_received':'sms_recevied'})
    mapp
    
6: Check and fix data types (e.g., age should be int, date as datetime).
      mapp['Scheduled_date'] = pd.to_datetime(mapp['Scheduled_date'])
      mapp['Appointment_date'] = pd.to_datetime(mapp['Appointment_date'])
      print("\nAfter datetime conversion:")
      print(mapp[['Scheduled_date', 'Appointment_date']].dtypes)
      mapp
