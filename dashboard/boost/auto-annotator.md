# Auto Annotator

The RedBrick AI Auto Annotator is an automated segmentation tool that allows teams to easily generate segmentation masks for hundreds of different structures on CT and MR images, which are then inserted into a Project pipeline as pre-labels.

To use Auto Annotator, you must have an [active Boost instance](./#creating-a-boost-instance) available in your Organization.

***

## Adding Auto Annotator to a Project

The decision to utilize Auto Annotator for a Project must be made **at Project creation.**&#x20;

After a Project has been created, there is no way to retroactively add Auto Annotator to it, as the model will be added to the Project pipeline as a pre-Stage.

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-18 at 16.15.36@2x.png" alt="" width="563"><figcaption><p>An example pipeline with Auto Annotator</p></figcaption></figure>

If you have an active Boost instance in your Organization, you will notice that Step (4) of standard Project creation looks slightly different:

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-18 at 16.01.07@2x.png" alt="" width="563"><figcaption><p>Project creation with Auto Annotator</p></figcaption></figure>

1. The Auto Annotator toggle;
2. Object Label mapping window;
3. Model URL selection dropdown;

### Mapping Object Labels

After you've enabled Auto Annotator in a Project, you must map the labels that the algorithm will generate to a corresponding entry in your Redbrick Taxonomy.

Click on **Map object labels** to open the Mapping window.

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-18 at 16.04.14@2x.png" alt=""><figcaption><p>The Mapping Window</p></figcaption></figure>

The Mapping Window allows you to:

1. Choose which Auto Annotator sub-type you would like to use for this specific Project;
2. Map the output of the designated model sub-type to the Object Labels of your Project's Taxonomy;

{% embed url="https://share.cleanshot.com/jpLLs897" %}
Mapping model output
{% endembed %}

Each entry in the Auto Annotator Labels list can only be mapped once. However, Taxonomy Labels can be mapped to as many structures as you'd like.

Consider the example below, where the model output for `kidney_right` and `kidney_left` are both mapped to a single RedBrick Object Label called `Kidney`.

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-18 at 16.12.14@2x (1).png" alt=""><figcaption></figcaption></figure>

Once you have finished mapping your labels, click on **Save changes**.

### Selecting a Model

If you have multiple models integrated with RedBrick AI, you can use the dropdown field to select which model should run on this specific Project.

***

## Running Auto Annotator in a Project

Once your Project is created, any [data that you upload](../../importing-data/uploading-data-to-redbrick.md) or [integrate](../../importing-data/import-cloud-data.md) to the Project will automatically pass through the Auto Annotator pre-Stage, where automated annotation will occur.

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-18 at 16.19.32@2x.png" alt=""><figcaption><p>4 Tasks in the Auto Annotator pre-Stage</p></figcaption></figure>

**There is nothing that the user needs to do for Tasks in the Auto Annotator pre-Stage.** After the Auto Annotator is done generating labels, the Task will automatically move to the next Stage in your Project pipeline.

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-18 at 16.21.02@2x.png" alt=""><figcaption><p>Task History of a Task that was labeled automatically</p></figcaption></figure>

Once the Tasks have reached the next Stage in your pipeline, your team can begin work on it.

## Boost Models

When creating a Project with [Auto Annotator](auto-annotator.md#adding-auto-annotator-to-a-project) enabled, you have the opportunity to select a wide range of potential segmentations for your pre-Stage. A comprehensive list of all libraries and structures can be found below.

### total

spleen\
kidney\_right\
kidney\_left\
gallbladder\
liver\
stomach\
pancreas\
adrenal\_gland\_right\
adrenal\_gland\_left\
lung\_upper\_lobe\_left\
lung\_lower\_lobe\_left\
lung\_upper\_lobe\_right\
lung\_middle\_lobe\_right\
lung\_lower\_lobe\_right\
esophagus\
trachea\
thyroid\_gland\
small\_bowel\
duodenum\
colon\
urinary\_bladder\
prostate\
kidney\_cyst\_left\
kidney\_cyst\_right\
sacrum\
vertebrae\_S1\
vertebrae\_L5\
vertebrae\_L4\
vertebrae\_L3\
vertebrae\_L2\
vertebrae\_L1\
vertebrae\_T12\
vertebrae\_T11\
vertebrae\_T10\
vertebrae\_T9\
vertebrae\_T8\
vertebrae\_T7\
vertebrae\_T6\
vertebrae\_T5\
vertebrae\_T4\
vertebrae\_T3\
vertebrae\_T2\
vertebrae\_T1\
vertebrae\_C7\
vertebrae\_C6\
vertebrae\_C5\
vertebrae\_C4\
vertebrae\_C3\
vertebrae\_C2\
vertebrae\_C1\
heart\
aorta\
pulmonary\_vein\
brachiocephalic\_trunk\
subclavian\_artery\_right\
subclavian\_artery\_left\
common\_carotid\_artery\_right\
common\_carotid\_artery\_left\
brachiocephalic\_vein\_left\
brachiocephalic\_vein\_right\
atrial\_appendage\_left\
superior\_vena\_cava\
inferior\_vena\_cava\
portal\_vein\_and\_splenic\_vein\
iliac\_artery\_left\
iliac\_artery\_right\
iliac\_vena\_left\
iliac\_vena\_right\
humerus\_left\
humerus\_right\
scapula\_left\
scapula\_right\
clavicula\_left\
clavicula\_right\
femur\_left\
femur\_right\
hip\_left\
hip\_right\
spinal\_cord\
gluteus\_maximus\_left\
gluteus\_maximus\_right\
gluteus\_medius\_left\
gluteus\_medius\_right\
gluteus\_minimus\_left\
gluteus\_minimus\_right\
autochthon\_left\
autochthon\_right\
iliopsoas\_left\
iliopsoas\_right\
brain\
skull\
rib\_left\_1\
rib\_left\_2\
rib\_left\_3\
rib\_left\_4\
rib\_left\_5\
rib\_left\_6\
rib\_left\_7\
rib\_left\_8\
rib\_left\_9\
rib\_left\_10\
rib\_left\_11\
rib\_left\_12\
rib\_right\_1\
rib\_right\_2\
rib\_right\_3\
rib\_right\_4\
rib\_right\_5\
rib\_right\_6\
rib\_right\_7\
rib\_right\_8\
rib\_right\_9\
rib\_right\_10\
rib\_right\_11\
rib\_right\_12\
sternum\
costal\_cartilages

### total\_MR

spleen\
kidney\_right\
kidney\_left\
gallbladder\
liver\
stomach\
pancreas\
adrenal\_gland\_right\
adrenal\_gland\_left\
lung\_left\
lung\_right\
esophagus\
small\_bowel\
duodenum\
colon\
urinary\_bladder\
prostate\
sacrum\
vertebrae\
intervertebral\_discs\
spinal\_cord\
heart\
aorta\
inferior\_vena\_cava\
portal\_vein\_and\_splenic\_vein\
iliac\_artery\_left\
iliac\_artery\_right\
iliac\_vena\_left\
iliac\_vena\_right\
humerus\_left\
humerus\_right\
scapula\_left\
scapula\_right\
clavicula\_left\
clavicula\_right\
femur\_left\
femur\_right\
hip\_left\
hip\_right\
gluteus\_maximus\_left\
gluteus\_maximus\_right\
gluteus\_medius\_left\
gluteus\_medius\_right\
gluteus\_minimus\_left\
gluteus\_minimus\_right\
autochthon\_left\
autochthon\_right\
iliopsoas\_left\
iliopsoas\_right\
brain

### **lung\_vessels**&#x20;

lung\_vessels (cite [paper](https://www.sciencedirect.com/science/article/pii/S0720048X22001097))\
lung\_trachea\_bronchia

### **body**&#x20;

body\
body\_trunc\
body\_extremities\
skin

### **body\_mr**

body\_trunc\
body\_extremities (for MR images)

### **vertebrae\_mr**&#x20;

sacrum\
vertebrae\_L5\
vertebrae\_L4\
vertebrae\_L3\
vertebrae\_L2\
vertebrae\_L1\
vertebrae\_T12\
vertebrae\_T11\
vertebrae\_T10\
vertebrae\_T9\
vertebrae\_T8\
vertebrae\_T7\
vertebrae\_T6\
vertebrae\_T5\
vertebrae\_T4\
vertebrae\_T3\
vertebrae\_T2\
vertebrae\_T1\
vertebrae\_C7\
vertebrae\_C6\
vertebrae\_C5\
vertebrae\_C4\
vertebrae\_C3\
vertebrae\_C2\
vertebrae\_C1

### **cerebral\_bleed**

intracerebral\_hemorrhage (cite [paper](https://www.mdpi.com/2077-0383/12/7/2631))

### **hip\_implant**

hip\_implant

### **pleural\_pericard\_effusion**&#x20;

pleural\_effusion (cite [paper](http://dx.doi.org/10.1097/RLI.0000000000000869))\
pericardial\_effusion (cite [paper](http://dx.doi.org/10.3390/diagnostics12051045))

### **Head\_glands\_cavities**&#x20;

eye\_left\
eye\_right\
eye\_lens\_left\
eye\_lens\_right\
optic\_nerve\_left\
optic\_nerve\_right\
parotid\_gland\_left\
parotid\_gland\_right\
submandibular\_gland\_right\
submandibular\_gland\_left\
nasopharynx, oropharynx\
hypopharynx \
nasal\_cavity\_right\
nasal\_cavity\_left\
auditory\_canal\_right\
auditory\_canal\_left\
soft\_palate\
hard\_palate (cite [paper](https://www.mdpi.com/2072-6694/16/2/415))

### **head\_muscles**

masseter\_right\
masseter\_left\
temporalis\_right\
temporalis\_left\
lateral\_pterygoid\_right\
lateral\_pterygoid\_left\
medial\_pterygoid\_right\
medial\_pterygoid\_left\
tongue\
digastric\_right\
digastric\_left

### **headneck\_bones\_vessels**

larynx\_air\
thyroid\_cartilage\
hyoid \
cricoid\_cartilage\
zygomatic\_arch\_right\
zygomatic\_arch\_left\
styloid\_process\_right\
styloid\_process\_left\
internal\_carotid\_artery\_right\
internal\_carotid\_artery\_left\
internal\_jugular\_vein\_right\
internal\_jugular\_vein\_left (cite [paper](https://www.mdpi.com/2072-6694/16/2/415))

### **headneck\_muscles**

sternocleidomastoid\_right\
sternocleidomastoid\_left\
superior\_pharyngeal\_constrictor\
middle\_pharyngeal\_constrictor\
inferior\_pharyngeal\_constrictor\
trapezius\_right\
trapezius\_left\
platysma\_right\
platysma\_left\
levator\_scapulae\_right\
levator\_scapulae\_left\
anterior\_scalene\_right\
anterior\_scalene\_left\
middle\_scalene\_right\
middle\_scalene\_left\
posterior\_scalene\_right\
posterior\_scalene\_left\
sterno\_thyroid\_right\
sterno\_thyroid\_left\
thyrohyoid\_right\
thyrohyoid\_left\
prevertebral\_right\
prevertebral\_left (cite [paper](https://www.mdpi.com/2072-6694/16/2/415))

### **liver\_vessels**

liver\_vessels \
liver\_tumor (cite [paper](https://arxiv.org/abs/1902.09063))

### **oculomotor\_muscles**:&#x20;

skull\
eyeball\_right\
lateral\_rectus\_muscle\_right\
superior\_oblique\_muscle\_right\
levator\_palpebrae\_superioris\_right\
superior\_rectus\_muscle\_right\
medial\_rectus\_muscle\_left\
inferior\_oblique\_muscle\_right\
inferior\_rectus\_muscle\_right\
optic\_nerve\_left\
eyeball\_left\
lateral\_rectus\_muscle\_left\
superior\_oblique\_muscle\_left\
levator\_palpebrae\_superioris\_left\
superior\_rectus\_muscle\_left\
medial\_rectus\_muscle\_right\
inferior\_oblique\_muscle\_left\
inferior\_rectus\_muscle\_left\
optic\_nerve\_right

### **lung\_nodules**

lung\
lung\_nodules (provided by [BLUEMIND AI](https://bluemind.co/): Fitzjalen R., Aladin M., Nanyan G.) (trained on 1353 subjects, partly from LIDC-IDRI)

### **kidney\_cysts**

kidney\_cyst\_left, kidney\_cyst\_right (strongly improved accuracy compared to kidney\_cysts inside of `total` task)

### **breasts**

breast
