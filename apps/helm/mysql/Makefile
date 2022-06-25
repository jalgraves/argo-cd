
name ?= mysql
port ?= 3306
tag ?= mysql:5.7.38-debian

## Install MySQL
mysql/install:
	helm upgrade --install $(name) mysql/ \
		--namespace database \
		--set image.tag=$(tag) \
		--set db_admin_pass=${DB_ADMIN_PASS} \
		--set db_admin_user=${DB_ADMIN_USER} \
		--set db_root_pass=${DB_ROOT_PASS} \
		--set community_forum_service_db_user=${COMMUNITY_FORUM_SERVICE_DB_USER} \
		--set community_forum_service_db_pass=${COMMUNITY_FORUM_SERVICE_DB_PASS} \
		--set community_forum_service_db_name=${COMMUNITY_FORUM_SERVICE_DB_NAME} \
		--set content_service_db_user=${CONTENT_SERVICE_DB_USER} \
		--set content_service_db_pass=${CONTENT_SERVICE_DB_PASS} \
		--set content_service_db_name=${CONTENT_SERVICE_DB_NAME} \
		--set feedback_service_db_user=${FEEDBACK_SERVICE_DB_USER} \
		--set feedback_service_db_pass=${FEEDBACK_SERVICE_DB_PASS} \
		--set feedback_service_db_name=${FEEDBACK_SERVICE_DB_NAME} \
		--set helpdesk_service_db_user=${HELPDESK_SERVICE_DB_USER} \
		--set helpdesk_service_db_pass=${HELPDESK_SERVICE_DB_PASS} \
		--set helpdesk_service_db_name=${HELPDESK_SERVICE_DB_NAME} \
		--set helix_db_user=${HELIX_DB_USER} \
		--set helix_db_pass=${HELIX_DB_PASS} \
		--set helix_db_name=${HELIX_DB_NAME} \
		--set helix_edge_db_user=${HELIX_EDGE_DB_USER} \
		--set helix_edge_db_pass=${HELIX_EDGE_DB_PASS} \
		--set helix_edge_db_name=${HELIX_EDGE_DB_NAME} \
		--set notifications_service_db_user=${NOTIFICATIONS_SERVICE_DB_USER} \
		--set notifications_service_db_pass=${NOTIFICATIONS_SERVICE_DB_PASS} \
		--set notifications_service_db_name=${NOTIFICATIONS_SERVICE_DB_NAME} \
		--set translation_service_db_user=${TRANSLATION_SERVICE_DB_USER} \
		--set translation_service_db_pass=${TRANSLATION_SERVICE_DB_PASS} \
		--set translation_service_db_name=${TRANSLATION_SERVICE_DB_NAME} \
		--set visitor_registration_service_db_user=${VISITOR_REGISTRATION_SERVICE_DB_USER} \
		--set visitor_registration_service_db_pass=${VISITOR_REGISTRATION_SERVICE_DB_PASS} \
		--set visitor_registration_service_db_name=${VISITOR_REGISTRATION_SERVICE_DB_NAME} \
		--set users_service_db_user=${USERS_SERVICE_DB_USER} \
		--set users_service_db_pass=${USERS_SERVICE_DB_PASS} \
		--set users_service_db_name=${USERS_SERVICE_DB_NAME} \
		--set pvc.enabled=true \
		--set istio.enabled=false \
		--set domain_name=pilot.use2.hqo.pub \
		--debug

mysql/template:
	helm template . \
		--namespace database \
		--name-template=$(name) \
		--set image.tag=$(tag) \
		--set db_admin_pass=${DB_ADMIN_PASS} \
		--set db_admin_user=${DB_ADMIN_USER} \
		--set db_root_pass=${DB_ROOT_PASS} \
		--set users_service_db_user=${USERS_SERVICE_DB_USER} \
		--set users_service_db_pass=${USERS_SERVICE_DB_PASS} \
		--set users_service_db_name=${USERS_SERVICE_DB_NAME} \
		--set pvc.enabled=false \
		--debug

db/port_forward:
		kubectl port-forward --namespace $(namespace) svc/$(name) $(port):$(port)

db/stop_pf:
		./scripts/stop_port_forward.sh $(port)

users_service:
	helm upgrade --install users-service hqo/users-service \
		--namespace pilot \
		--set envVariables.DB_HOST=mysql.database \
		--set envVariables.DB_PASS=uLdaCwXV6wPis8Ww9FWxfA7H2EH43cqU \
		--set envVariables.DB_USER=users_service
