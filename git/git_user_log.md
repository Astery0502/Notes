# Logs, problems, tricks and tips when using git #

## 1. delete the plug dir in the two branches ##

When starting one branch, the branch head tracks the current commit and the unworking branch not.  
And while switching among branches, Git read the commit object and restore the objects in the tree object in the according commit object. In the object database, Git add to the objects once any is adding or modified, thus there is impossible that doing with the content of the object leading to both changes of the references in both branches pointed to the object.  
At last, it is the dir not under Git which is independent of the VCS.  
