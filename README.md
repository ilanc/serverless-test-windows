# Serverless on windows

### 1. executable permissions inside .serverless/{package}.zip
* initially it appeared that any serverless deployments on windows would not set +x permission for bundled linux binaries
	* see original serverless issue [here](https://github.com/serverless/serverless/issues/3557)
* on investigation it appears:
	* [wsl](https://msdn.microsoft.com/en-us/commandline/wsl/about) sets permissions to rwxrwxrwx (i.e. 777)
		* see `.\.serverless.wsl.nopermissions\hello.zip`
	* [gitbash](https://git-scm.com/download/win) (a type of [msysgit](https://stackoverflow.com/questions/22310007/differences-between-git-scm-msysgit-git-for-windows)) sets permissions to rw-rw-rw- (i.e. 666)
		* see `.\.serverless.gitbash.nopermissions\hello.zip`
	* cmd.exe sets permissions to rw-rw-rw- (i.e. 666)
		* see `.\.serverless.cmd.nopermissions\hello.zip`
* solution
	* unfortunately I wasted time developing [this](https://github.com/ilanc/serverless/commit/fa3b00f2255bc9693fd9b7238c3524ed9d3d317f)
	* a simpler solution is just to always build in [wsl](https://msdn.microsoft.com/en-us/commandline/wsl/about) on windows