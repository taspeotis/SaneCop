SaneCop is a settings file for [StyleCop](http://stylecop.codeplex.com/) that disables some default rules to allow you to write concise (but readable) code.

# Example

This example assumes the following file and directory structure:

    YourApplication\Solution.sln
    YourApplication\Project\Project.csproj

**Step 1: Add SaneCop as a Git submodule**

    cd YourApplication
    git submodule add git://github.com/taspeotis/SaneCop.git SaneCop

Your file and directory structure should now look like this:

    YourApplication\Solution.sln
    YourApplication\Project\Project.csproj
    YourApplication\SaneCop\...

**Step 2: Create a solution-wide `Settings.StyleCop` file**

Create a file called `Settings.StyleCop` in the root the solution directory. The file will include any solution-wide StyleCop settings you need to apply, and merge in SaneCop's rules.

    <StyleCopSettings Version="105">
      <GlobalSettings>
        <StringProperty Name="LinkedSettingsFile">..\SaneCop\Settings.StyleCop</StringProperty>
        <StringProperty Name="MergeSettingsFiles">Linked</StringProperty>
      </GlobalSettings>
      <Analyzers>
        <Analyzer AnalyzerId="StyleCop.CSharp.DocumentationRules">
          <AnalyzerSettings>
            <StringProperty Name="CompanyName">Your Company Name</StringProperty>
            <StringProperty Name="Copyright">Your Copyright</StringProperty>
          </AnalyzerSettings>
        </Analyzer>
      </Analyzers>
    </StyleCopSettings>

Note that `GlobalSettings` is responsible for merging in SaneCop's rules, the `Analyzers` section is given as an example of setting solution-wide StyleCop settings. (It is shown for completeness' sake.)

Further note that the path to SaneCop is given as `..\SaneCop` not `SaneCop`, even though `SaneCop` is the relative path from the `Settings.StyleCop` file. See [Work Item 7145](http://stylecop.codeplex.com/workitem/7145) for more information.

Your file and directory structure should now look like this:

    YourApplication\Solution.sln
    YourApplication\Settings.StyleCop
    YourApplication\Project\Project.csproj
    YourApplication\SaneCop\...

**Step 3: Run StyleCop**

You can now run StyleCop with SaneCop's settings file applied. If SaneCop's settings aren't in effect you may need to review each project's StyleCop settings to ensure that their settings file is configured to *Merge with settings file found in parent folders*. See [Sharing StyleCop Settings Across Projects](http://blogs.msdn.com/b/sourceanalysis/archive/2008/05/25/sharing-source-analysis-settings-across-projects.aspx) for more information.