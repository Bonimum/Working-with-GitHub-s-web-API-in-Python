### Requesting data using an API call

```bash
https://api.github.com/search/repositories?q=language:python&sort=stars
```


### Installing requests

```python
pip install --user requests
```
### Processing an API response

```python
import requests

# Make an API request 
url = 'https://api.github.com/search/repositories?q=language:python&sort=stars'
j = requests.get(url)
print("Status code:", j.status_code)
# In a variable, save the API response.
respons_dict = j.json()
# Evaluate the results.
print(respons_dict.keys())
```

### Using the response dictionary
```python
import requests

# Make an API call 
url = 'https://api.github.com/search/repositories?q=language:python&sort=stars'
j = requests.get(url)
print("Status code:", j.status_code)
# In a variable, save the API response.
respons_dict = j.json()
print("Total repositories:", respons_dict['total_count'])
# Explore information about the repositories.
repos_dicts = respons_dict['items']
print("Repositories found:", len(repos_dicts))
# Examine the first repository.
repos_dict = repos_dicts[0]
print("Keys:", len(repos_dict))
for key in sorted(repos_dict.keys()):
 print(key)
```


The GitHub API returns a range of data for each repository: `repos_dict` has `74` keys. You may get a sense of the type of information you can get about a project by observing these keys.

Let's look at some of the keys in `repos_dict` and see what they mean:

```python
import requests

# Make an API call 
url = 'https://api.github.com/search/repositories?q=language:python&sort=stars'
j = requests.get(url)
print("Status code:", j.status_code)
# Store API response in a variable.
respons_dict = j.json()
print("Total repositories:", respons_dict['total_count'])

# Explore information about the repositories.
repos_dicts = respons_dict['items']
print("Repositories returned:", len(repos_dicts))
# Examine the first repository.
repos_dict = repos_dicts[0]
print("\nThe following is some information regarding the first repository:")
print('Name:', repos_dict['name'])  #print the name of the project
print('Owner:', repos_dict['owner']['login'])  #use the key owner and the the key login to access the dictionary representing the owner and the owner’s login name respectively.
print('Stars:', repos_dict['stargazers_count'])  #print how many stars the project has earned
print('Repository:', repos_dict['html_url'])  #print URL for the project’s GitHub repository
print('Created:', repos_dict['created_at'])  #print when it was created
print('Updated:', repos_dict['updated_at'])  #show when it was last updated
print('Description:', repos_dict['description']) #print the repository’s description

```



### Summarizing the top repositories
```python
import requests
url = 'https://api.github.com/search/repositories?q=language:python&sort=stars'
r = requests.get(url)
print("Status code:", r.status_code)
respons_dict = r.json()
print("Total repositories:", respons_dict['total_count'])

repos_dicts = respons_dict['items']
print("Repositories returned:", len(repos_dicts))
print("\nSelected information about each repository:")
for repos_dict in repos_dicts:   #loop through all the dictionaries in repo_dicts.
    print('\nName:', repos_dict['name'])
    print('Owner:', repos_dict['owner']['login'])
    print('Stars:', repos_dict['stargazers_count'])
    print('Repository:', repos_dict['html_url'])
    print('Description:', repos_dict['description'])

```







