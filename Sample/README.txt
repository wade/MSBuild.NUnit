﻿This snippet of Project XML was hand-added to the Sample.csproj file to 
configure the build to execute NUnit tests.

  <UsingTask AssemblyFile="..\MSBuild.NUnit\bin\$(Configuration)\MSBuild.NUnit.dll" TaskName="MSBuild.Tasks.NUnit" />
  <Target Name="RunUnitTest">
	<NUnit Assemblies="$(ProjectName).csproj" ToolPath="..\packages\NUnit.Runners.2.6.2\tools" DisableShadowCopy="true" Force32Bit="false" ProjectConfiguration="$(Configuration)" FrameworkToUse="net-3.5" WorkingDirectory="$(ProjectDir)" ContinueOnError="false" ProcessModel="Single" HideDots="true" />
  </Target>
  <Target Name="AfterBuild" DependsOnTargets="RunUnitTest">
  </Target>

TWO IMPORTANT NOTES:

1) You can easily make the unit testing run for some specific configuration or other condition by adding a Condition attribute to the RunUnitTest target
2) In the example above NUnit isn't side-installed with MSBuild.NUnit.dll so the ToolPath attribute was used with a hard-reference to a NUnit installation.
For my usage I have a Dependencies\NUnit folder inside the solution folder for a big solution with many projects and many unit-test projects, that is sent up
to the version control repository which contains a copy the bin\(framework)\ of the latest NUnit install and the NUnit task dll, so a relative path, or
solution-rooted path to the MSBuild.NUnit.dll there is enough to make things work nicely, without the hardcoded ToolPath.
