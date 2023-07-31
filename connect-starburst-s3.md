# Setting up your environment with Starburst and Amazon S3

##### Requirements:

- RHODS working cluster with administrator access
- Startburst Enterprise licence [optional when using demo.redhat.com [workshop](https://demo.redhat.com/catalog?item=babylon-catalog-prod/sandboxes-gpte.ocp4-workshop-fraud-detection.prod&utm_source=webapp&utm_medium=share-link)]
- Write access to your own Amazon S3 bucket [optional when using demo.redhat.com [workshop](https://demo.redhat.com/catalog?item=babylon-catalog-prod/sandboxes-gpte.ocp4-workshop-fraud-detection.prod&utm_source=webapp&utm_medium=share-link)]
- Access to the [original dataset](https://drive.google.com/file/d/1YhmV3vPbFe-JXU_biwvaizV0WGhAegH1/view) [optional when using demo.redhat.com [workshop](https://demo.redhat.com/catalog?item=babylon-catalog-prod/sandboxes-gpte.ocp4-workshop-fraud-detection.prod&utm_source=webapp&utm_medium=share-link)]

#### What is Trino and Starburst Enterprise?

Trino (formerly Presto® SQL) is the fastest open source, massively parallel
processing SQL query engine designed for analytics of large datasets distributed
over one or more data sources in object storage, databases and other systems.

Starburst Enterprise platform (SEP) is a fully supported, enterprise-grade
distribution of Trino. It adds integrations, improves performance, provides
security, and makes it easy to deploy, configure and manage your clusters.

### Goal

In this document we will cover how to work with the data of the fraud-detection
example with SQL-like queries and an instance of SEP running in the Red Hat
Openshift Data Science cluster.

### Steps:

1. Store the original data in S3 [optional when using demo.redhat.com [workshop](https://demo.redhat.com/catalog?item=babylon-catalog-prod/sandboxes-gpte.ocp4-workshop-fraud-detection.prod&utm_source=webapp&utm_medium=share-link)]

    Upload the
file [creditcard_with_empty_values.csv](https://drive.google.com/file/d/1YhmV3vPbFe-JXU_biwvaizV0WGhAegH1/view)
to a bucket called `<PASTE_HERE_YOUR_BUCKET_NAME>/data`. In this example, we will name it `rhods-fraud-detection`.
Your AWS credentials **must** have read and write access to this bucket.

2. Set credentials and configure Starburst Enterprise [optional when using demo.redhat.com [workshop](https://demo.redhat.com/catalog?item=babylon-catalog-prod/sandboxes-gpte.ocp4-workshop-fraud-detection.prod&utm_source=webapp&utm_medium=share-link)]


    1. Go to the configs directory `cd ./configs`
    2. Update the [01_starburst_licence.yaml](configs/01_starburst_licence.yaml) file with your own Startbust Enterprise license. 
    3. Update the [02_aws_credentials.yaml](configs/02_aws_credentials.yaml) file with your own Amazon credentials.
    4. Apply the configuration files `cat *.yaml | oc apply -f -`
        <details>
            <summary>Expected output</summary>
        
        ```bash
        $: cat *.yaml | oc apply -f -
        secret/starburstdata created
        secret/aws-credentials created
        starburstenterprise.charts.starburstdata.com/starburstenterprise created
        starbursthive.charts.starburstdata.com/starbursthive created
        route.route.openshift.io/starburst-web created
        ```
        </details>
