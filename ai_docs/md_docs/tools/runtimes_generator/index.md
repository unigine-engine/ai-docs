# Runtimes Generator

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


Normally the `.runtimes` folder content is updated automatically when you open the UnigineEditor. The **Runtimes Generator** is a console tool enabling you to generate [runtimes](../../editor2/assets_workflow/assets_runtimes.md) without running the Editor, right from the command line. This tool might be useful for example, when only your assets are managed by a [VCS](../../editor2/assets_workflow/version_control/index.md), and you'd like to trigger generation of the `.runtimes` folder content right after checking out the latest version from the repository and then run your application. To invoke the tool and generate your runtimes, run `<UnigineSDK>/bin/RuntimesGenerator_x64` from the command prompt (no additional arguments required).


Upon successful completion of the generation process the contents of the `.runtimes` folder shall be updated in accordance with the assets inside the `data` folder.
