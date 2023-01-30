# Part A
## Question 1
>--iidfile string: - Write the image ID to the file

Based on [Docker Documentation][https://docs.docker.com/engine/reference/commandline/image_build/]

## Question 2
Command
```
$ docker run -it --entrypoint bash python:3.9
```

## Question 3
```sql
SELECT COUNT(*)
FROM green_taxi_trips
WHERE DATE(lpep_pickup_datetime) = '2019-01-15'
```

## Question 4
```sql
SELECT lpep_pickup_datetime FROM green_taxi_trips 
WHERE trip_distance = (SELECT MAX(trip_distance) as max_distance FROM green_taxi_trips)
```
											
## Question 5		   
```sql		   
SELECT passenger_count, COUNT(*) as trip_count
FROM green_taxi_trips 
WHERE passenger_count in (2,3)
AND DATE(lpep_pickup_datetime) = '2019-01-01'
GROUP BY passenger_count
```

## Question 6	
```sql
SELECT z."Zone" FROM green_taxi_trips t
LEFT JOIN taxi_zone z on t."DOLocationID" = z."LocationID"
WHERE tip_amount = (SELECT MAX(tip_amount) FROM green_taxi_trips t
					LEFT JOIN taxi_zone z on t."PULocationID" = z."LocationID"
					WHERE z."Zone" = 'Astoria')
```


# Part B
Command
>linh_d_pham90@cloudshell:~/.../Week_1/GCP_Terraform (sylvan-journey-1710)$ terraform apply
var.project
  Your GCP Project ID

  Enter a value: sylvan-journey-1710

Output
```
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # google_bigquery_dataset.dataset will be created
  + resource "google_bigquery_dataset" "dataset" {
      + creation_time              = (known after apply)
      + dataset_id                 = "trips_data_all"
      + delete_contents_on_destroy = false
      + etag                       = (known after apply)
      + id                         = (known after apply)
      + labels                     = (known after apply)
      + last_modified_time         = (known after apply)
      + location                   = "europe-west6"
      + project                    = "sylvan-journey-1710"
      + self_link                  = (known after apply)

      + access {
          + domain         = (known after apply)
          + group_by_email = (known after apply)
          + role           = (known after apply)
          + special_group  = (known after apply)
          + user_by_email  = (known after apply)

          + dataset {
              + target_types = (known after apply)

              + dataset {
                  + dataset_id = (known after apply)
                  + project_id = (known after apply)
                }
            }

          + routine {
              + dataset_id = (known after apply)
              + project_id = (known after apply)
              + routine_id = (known after apply)
            }

          + view {
              + dataset_id = (known after apply)
              + project_id = (known after apply)
              + table_id   = (known after apply)
            }
        }
    }

  # google_storage_bucket.data-lake-bucket will be created
  + resource "google_storage_bucket" "data-lake-bucket" {
      + force_destroy               = true
      + id                          = (known after apply)
      + location                    = "EUROPE-WEST6"
      + name                        = "dtc_data_lake_sylvan-journey-1710"
      + project                     = (known after apply)
      + public_access_prevention    = (known after apply)
      + self_link                   = (known after apply)
      + storage_class               = "STANDARD"
      + uniform_bucket_level_access = true
      + url                         = (known after apply)

      + lifecycle_rule {
          + action {
              + type = "Delete"
            }

          + condition {
              + age                   = 30
              + matches_prefix        = []
              + matches_storage_class = []
              + matches_suffix        = []
              + with_state            = (known after apply)
            }
        }

      + versioning {
          + enabled = true
        }

      + website {
          + main_page_suffix = (known after apply)
          + not_found_page   = (known after apply)
        }
    }

Plan: 2 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

google_bigquery_dataset.dataset: Creating...
google_storage_bucket.data-lake-bucket: Creating...
google_bigquery_dataset.dataset: Creation complete after 1s [id=projects/sylvan-journey-1710/datasets/trips_data_all]
google_storage_bucket.data-lake-bucket: Creation complete after 2s [id=dtc_data_lake_sylvan-journey-1710]

Apply complete! Resources: 2 added, 0 changed, 0 destroyed.
```
