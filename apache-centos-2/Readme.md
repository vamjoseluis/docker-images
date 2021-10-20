This is an example of a docker file with Centos and apache

#Docker - Best Practices
- Ephemeral. The service should be easy to destroy
- One service per image/container (by instace apache and mysql)
- Add undesirable files to the .dockerignore to reduce image's size
- Try to use the less layers as you can
- Split arguments in different lines to make it more redeable
- Not to install unnecessary packages
- User LABELS to add metadata
