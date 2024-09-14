By default, Ansible executes each task on the managed nodes only if that particular task is complete and successful.
 
for example, there are 3 managed nodes or servers, and we have 2 different tasks to execute on these 3 managed nodes.

According to Ansible's execution nature, 
1. Only if the first task is complete and successful on all three nodes will it execute the second task.
2. If a task fails only on Node 1 and succeeds on Node 2 and Node 3, Ansible will NOT run the next tasks ONLY on Node 1. Because the task is successful on Node 2 and Node 3, Ansible will execute the next tasks on Node 2 and Node 3.

By keeping this in mind, we have a concept called ERROR HANDLING:

To handle these types of errors in Ansible, we use [ignore_errors: yes]




TASK: Install Docker by following these steps. (use error handling concept to ignore errors and execute tasks)

Task 1: Check if OpenSSH & OpenSSL packages exist on the managed nodes. If yes, then make sure the packages are the latest version. If not, then no worries. just ignore.

Task 2: Verify if Docker is installed on the managed nodes. (If not installed then run task3)

Task 3: Install Docker. 




Note:

docker.io: Community-maintained and may not always be up-to-date or available for all Ubuntu versions.
docker-ce: Officially maintained by Docker and recommended for the latest versions, security patches, and features.

If you're okay with using an older version of Docker and want to use docker.io, you can verify if it's available on your EC2 instances by running:
sudo apt update && sudo apt-cache policy docker.io

If it is available, you can still proceed with the docker.io package in your playbook. Otherwise, stick with the official docker-ce installation method for the latest Docker version. 

If you prefer not to use external roles, the steps involving adding the GPG key, repository, and prerequisites are necessary for installing Docker CE manually, better use Ansible Galaxy roles.
