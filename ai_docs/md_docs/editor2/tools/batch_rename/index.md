# Batch Rename


The **Batch Rename** tool is designed to allow you quickly and easily rename numerous elements available in the *World Nodes, Properties, Materials* hierarchy windows, as well as assets in the *Asset Browser*.


To open the **Batch Rename** window, click *Tools -> Batch Rename* or right-click on an element in the Asset Browser or any hierarchy window and select *Batch Rename* in the [context menu](../../../editor2/interface/context/index.md).


The following options are available:


| Rename | [![](rename.png)](rename.png) | Rename the selected node(s), propertie(s), material(s) or file(s) to the specified name. > **Notice:** In case multiple files (properties, materials, or other assets) are selected, indices will be added to names automatically. However, **indices are not added for nodes**. |
|---|---|---|
| Set Prefix | [![](prefix.png)](prefix.png) | Add the specified prefix to the selected element(s). |
| Set Suffix | [![](suffix.png)](suffix.png) | Add the specified postfix to the selected element(s). |
| Find And Replace | [![](find_replace.png)](find_replace.png) | Find the specified combination of symbols and replace it as defined in the *Replace* field taking into account the *Case Sensitive* condition: - ***Override Original Case*** � replaces the combination of symbols in all names regardless of the case originally used in the name. - ***Rename Only The Same Case*** � replaces the combination of symbols with the same case as specified in the *Find* field. |
| Change Case | [![](change_case.png)](change_case.png) | Change the letter case in the name of the selected element(s) according to the selected condition: - ***Lower Case*** � any letters in the capital case are changed to the lower case. - ***Upper Case*** � any letters in the lower case are changed to the capital case. - ***Title Case*** � the first letter is in the capital case and all the rest are in the lower case. - ***Title Case For Each Word*** � the first letter of each word is in the capital case and all other letters are in the lower case. The word is a combination of letters separated from other combinations by a space or a non-letter symbol. |
