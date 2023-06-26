Submit a Python script using Hail Batch on the command line:
```
python3 myscript.py
```

Hail Batch setup in Python script:
(Note: the backend `regions` is normally set to `["us-central1"]`)
```
backend = hb.ServiceBackend(billing_project=your-billing-project,
                                remote_tmpdir=your-cloud-directory,
                                regions=cloud-region)

batch = hb.Batch(backend=backend, name=DEFAULT_BATCH_NAME,
                 default_image=your-Docker-image,  
                 default_cpu=request-cpu,
                 default_memory=request-memory)
```
Read a cloud file (localize the file to the container):
```
example_file = batch.read_input($cloud-file-path$)
```

Execute a bash job where the contents of the `example_file` is saved temporarily on Hail Batch:
```
batch_job = batch.new_job(name="new_job")
batch_job.command(f"cat {example_file} > batch_job.ofile")
```

Save the contents of the `example_file` to a cloud path:
```
batch.write_output(batch_job.ofile, "output-cloud-path")
```
