# Fake-Job_Scraper
This is a Repository to show an example of using the BeautifulSoup4 Tool to automate a job search
This automation tool is used to scrape specific job opportunities from a job search website. Proper use of this automation tool will filter and place jobs in a clean and neat list which will include the job title, the company, and the job's location. Also, this automation tool will provide individual links that will direct you toward the application site.  

This automation scraper makes use of the ‘BeautifulSoup4’ and ‘Requests’ tools that are used for its automation. It is also benefited by implementing the ‘Prettify’ tool to display the jobs in a list that will be clear and precise for the user to read, along with ‘Strip’ to ensure only the needed information from the job description is printed.  

REQUIRED INSTALLATION:  

To successfully run this program, users will need to first ensure that ‘Python3’ is properly installed and updated on the system. Developers can install Python directly from the Python home website: https://www.python.org/downloads/ 

After download completion, be sure to verify you have installed the latest version of Python by opening the terminal, entering the following command, and hitting enter: ~ % Python 

Terminal should display Python version – Python 3.9.7 


====================================================================================================


Install and import the following tools: 

- Requests 

- BeautifulSoup4 (bs4) 

Grabbing the ‘Requests’ tool: 

If you are writing the script using Pythons PyCharm Environment, then you can directly install the tool into your session by typing - import requests 

Grabbing the ‘BeautifulSoup4’ tool: 

Same previous steps will apply when installing ‘bs4’  


=====================================================================================================



SCRIPT EXAMPLE:


import requests
from bs4 import BeautifulSoup

URL = 'https://realpython.github.io/fake-jobs/'
page = requests.get(URL)

soup = BeautifulSoup(page.content, 'html.parser')
results = soup.find(id='ResultsContainer')
print(results.prettify())

job_elements = results.find_all('div', class_ = 'card-content')
for job_element in job_elements:
    print(job_element, end='\n'*2)

for job_element in job_elements:
    title_element = job_element.find('h2', class_ = 'title')
    company_element = job_element.find('h3', class_ = 'company')
    location_element = job_element.find('p', class_ = 'location')
    print(title_element.text.strip())
    print(company_element.text.strip())
    print(location_element.text.strip())
    print()

python_jobs = results.find_all('h2', string = 'Python')
print(python_jobs)

python_jobs = results.find_all(
    'h2', string = lambda text : 'python' in text.lower()

)

print(len(python_jobs))

python_jobs = results.find_all(
    'h2', string = lambda text : 'python' in text.lower()
)

python_job_elements = [
    h2_element.parent.parent.parent for h2_element in python_jobs
]

for job_element in python_job_elements:
    links = job_element.find_all('a')
    for link in links:
        link_url = link['href']
        print(f'Apply here: {link_url}\n')
        
        
======================================================================================================



<img width="471" alt="Screen Shot 2022-05-01 at 10 59 43 AM" src="https://user-images.githubusercontent.com/104590889/166154293-34d24d79-bc50-4afc-8d8d-d25fa351714f.png">





======================================================================================================
