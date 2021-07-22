SECRET_PATH=secret/cryoem/cryoem-daq--dev

etc:
	mkdir -p etc

passwords: etc
	# db
	vault kv get --field=root-password -format=json $(SECRET_PATH)/postgres | sed -e 's/\"//g' > etc/root-password
	vault kv get --field=primary-password -format=json $(SECRET_PATH)/postgres | sed -e 's/\"//g' > etc/primary-password
	vault kv get --field=user-password -format=json $(SECRET_PATH)/postgres | sed -e 's/\"//g' > etc/password
	# redis
	vault kv get --field=redis-password -format=json $(SECRET_PATH)/redis | sed -e 's/\"//g' > etc/redis-password
	# airflow
	vault kv get --field=fernet-key -format=json $(SECRET_PATH)/airflow | sed -e 's/\"//g' > etc/fernet-key
	vault kv get --field=auth -format=json $(SECRET_PATH)/airflow | sed -e 's/\"//g' > etc/auth
    
apply:
	kubectl apply -k .
