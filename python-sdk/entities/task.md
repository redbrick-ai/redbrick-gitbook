# Task

The Task module is an interface for labeling tasks in the pipeline. Each datapoint \(a single image or video\) is converted into Tasks inside a pipeline. The task module contains all the relevant information needed to perform labeling on a datapoint.

```python
redbrick.entity.task.Task()
```

{% tabs %}
{% tab title="Members" %}
| Member | Description |
| :--- | :--- |
| `task_id: str` | The unique task id of this task. |
| `dp_id: str` | The unique datapoint id of datapoint associated with this task. |
| `items_list: List[str]` | A list of the urls uploaded in the form of an [Items List](https://docs.redbrickai.com/platform/warehouse/prepare-data/prepare-your-items-list). |
| `items_list_presigned: List[str]` | The same list above, but with pre-signed urls if the storage method you're using requires authentication |
| `task_data_type: str` | The task type and data type of this task, e.g. `IMAGE_BBOX`, `VIDEO_CLASSIFY` etc. |
{% endtab %}

{% tab title="Methods" %}
| Method | Description |
| :--- | :--- |
| `get_data(presigned_url: str)` | Retrieves the image/frame data at the `presigned_url`, and returns a Numpy ndarray with RGB data. |
{% endtab %}
{% endtabs %}

