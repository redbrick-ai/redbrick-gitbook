# Create a project

Programmatically create a project using the RedBrick AI SDK, using the `create_project` method.  Perform standard set-up to create an RBOrganization object.

```python
import redbrick

# Standard Setup
api_key = "<TODO>"
url = "https://api.redbrickai.com"
org_id = "<TODO>"

organization = redbrick.get_org(api_key, url, org_id)
```

Create a project within your organization

```python
organization.create_project(
    # This is a unique name for your project
    name="TODO",
    
    # Defines the type of project.
    # for e.g. redbrick.LabelType.IMAGE_BBOX
    label_type="TODO"
    
    # Taxonomy name for this project. See all taxonomies within the 
    # taxonomy tab on the platform. 
    taxonomy_name="TODO", 
    
    # Number of reviews after the labeling step.
    reviews=2
)
```
