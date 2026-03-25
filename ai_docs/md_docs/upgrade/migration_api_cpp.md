# API Migration (CPP)


## Major Changes


- Added a new *[GlobalConfig](../api/library/engine/class.globalconfig_cpp.md)* class.
- Added a new *[DataBridge::Manager](../api/library/plugins/databridge/class.databridge_manager_cpp.md)* class.
- Added a new *[DataBridgeUI](../api/library/plugins/databridge/class.databridgeui_cpp.md)* class.
- Added a new *[DBVariable](../api/library/plugins/databridge/class.dbvariable_cpp.md)* class.
- Added a new *[NetworkInstance](../api/library/plugins/databridge/class.networkinstance_cpp.md)* class.
- Added a new *[NetworkManager](../api/library/plugins/databridge/class.networkmanager_cpp.md)* class.
- Added a new *[Server](../api/library/plugins/databridge/class.server_cpp.md)* class.
- Added a new *[Client](../api/library/plugins/databridge/class.client_cpp.md)* class.
- Added a new *[Sql](../api/library/plugins/sql/class.sql_cpp.md)* class.
- Added a new *[SqlDatabase](../api/library/plugins/sql/class.sqldatabase_cpp.md)* class.
- Added a new *[SqlRequest](../api/library/plugins/sql/class.sqlrequest_cpp.md)* class.
- Added a new *[SqlResponse](../api/library/plugins/sql/class.sqlresponse_cpp.md)* class.
- Added a new *[PathWildcards](../api/library/common/class.pathwildcards_cpp.md)* class.
- Added a new *[PDFFile](../api/library/plugins/pdfrender/class.pdffile_cpp.md)* class.
- Added a new *[PDFRender::Manager](../api/library/plugins/pdfrender/class.pdfrender_manager_cpp.md)* class.
- Added a new *[ProfilerDump](../api/library/engine/class.profilerdump_cpp.md)* class.
- Added a new *[ThreadsPool](../api/library/common/mt/class.threadspool_cpp.md)* class.
- Added a new *[AsyncTaskCallable](../api/library/common/mt/class.asynctaskcallable_cpp.md)* class.
- Added a new *[CPUTask](../api/library/common/mt/class.cputask_cpp.md)* class.
- Added a new *[Skeleton](../api/library/animations/skeletal/class.skeleton_cpp.md)* class.
- Added a new *[SkeletonPoseDecomposed](../api/library/animations/skeletal/class.skeletonposedecomposed_cpp.md)* class.
- Added a new *[SkeletonPoseMatrix](../api/library/animations/skeletal/class.skeletonposematrix_cpp.md)* class.
- Added a new *[SkeletonRetargeter](../api/library/animations/skeletal/class.skeletonretargeter_cpp.md)* class.
- Added a new *[SkeletonRetargeterEquals](../api/library/animations/skeletal/class.skeletonretargeterequals_cpp.md)* class.
- Added a new *[SkeletonRetargeterNamesMatching](../api/library/animations/skeletal/class.skeletonretargeternamesmatching_cpp.md)* class.
- Added a new *[SkeletonRetargeterTranslations](../api/library/animations/skeletal/class.skeletonretargetertranslations_cpp.md)* class.
- Added a new *[MeshSkinned](../api/library/rendering/class.meshskinned_cpp.md)* class.
- Added a new *[MeshSkinnedAnimation](../api/library/rendering/class.meshskinnedanimation_cpp.md)* class.
- Added a new *[NodeSkeletonPose](../api/library/nodes/class.nodeskeletonpose_cpp.md)* class.
- Added a new *[AnimScript](../api/library/animations/skeletal/class.animscript_cpp.md)* class.
- Added a new *[ImportMeshSkinned](../api/library/common/import/class.importmeshskinned_cpp.md)* class.
- Added a new *[ImportSkeleton](../api/library/common/import/class.importskeleton_cpp.md)* class.
- Added a new *[MediaPlayer::Manager](../api/library/plugins/mediaplayer/class.mediaplayer_manager_cpp.md)* class.
- Added a new *[MediaPlayer::VideoSource Class](../api/library/plugins/mediaplayer/class.mediaplayer_videosource_cpp.md)* class.
- Added a new *[VideoSourceComponent](../api/library/plugins/mediaplayer/class.videosourcecomponent_cpp.md)* class.
- Renamed the *WorldTransformBone* class as *[WorldTransformJoint](../api/library/worlds/class.worldtransformjoint_cpp.md)* class.
- Renamed the *BonesRetargeting* class as *[SkeletonRetargeter](../api/library/animations/skeletal/class.skeletonretargeter_cpp.md)* class.
- The *ObjectMeshSkinned* class has been renamed as *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cpp.md)*. A new simplified *[ObjectMeshSkinned](../api/library/objects/class.objectmeshskinned_cpp.md)* class has been added.
- The *PoolCPUShaders* class has been removed.


### IG-Related Changes


- The *IG::Converter* class has been split into two classes: Due to this, the return value of *[IG::Manager::getConverter()](../api/library/plugins/ig/api/class.managerinterface_cpp.md#getConverter_Converter)* has been changed to *Geodetics::Converter* to minimize manual migration, for cases related to axis conversions NED to ENU and ENU to NED, use the *[IG::Manager::getNEDConverter()](../api/library/plugins/ig/api/class.managerinterface_cpp.md#getNEDConverter_NEDConverter)* method instead.

  - *[Geodetics::Converter](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md)* - the class of the *[Geodetics](../api/library/geodetics/geodetics_plugin/index.md)* plugin containing most methods of the former *IG::Converter* class.
  - *[IG::NEDConverter](../api/library/plugins/ig/api/class.nedconverter_cpp.md)* - a new class containing methods for axis conversions NED to ENU and ENU to NED.
- The *GeodeticsTransformer* class has been moved to the *[Geodetics](../api/library/geodetics/geodetics_plugin/index.md)* plugin. Relevant changes include: | UNIGINE 2.20 | UNIGINE 2.21 | |---|---| | *`UnigineGeodeticsTransformer.h`* | Changed to `plugins/Unigine/Geodetics/UnigineGeodetics.h` | | ***UnigineGeodetics.h*** | Renamed to `UnigineGeodeticPivot.h` (the *[GeodeticPivot](../api/library/geodetics/class.geodeticpivot_cpp.md)* class API is unchanged). | | Complex initialization process: ```cpp auto transformer = GeodeticsTransformer::get(); if (!transformer) { Log::warning("Can't get transformer\n"); return 0; } int epsg_code = 3857; // EPSG Geodetic Parameter Dataset code dvec3 geodetic_origin = dvec3_zero; dvec3 original_geo_pos = dvec3(35.105580, -89.966775, 0.0); dvec3 world_pos, geo_pos; // setup projection transformer->setProjectionEpsg(epsg_code, geodetic_origin); // geodetic to world world_pos = transformer->geodeticToWorld(original_geo_pos).getTranslate(); // world to geodetic geo_pos = transformer->worldToGeodetic(world_pos); ``` | Simpler initialization for a georeferenced world - a world having an enabled [Geodetic Pivot](../objects/geodetics/geodeticpivot/index.md) or a [Sandworm](../editor2/sandworm/index.md)-generated terrain: ```cpp Unigine::Math::dvec3 original_geo_pos = Unigine::Math::dvec3(35.105580, -89.966775, 0.0); Unigine::Math::dvec3 world_pos, geo_pos; world_pos = Unigine::Plugins::Geodetics::Converter::get()->geodeticToWorld(original_geo_pos); geo_pos = Unigine::Plugins::Geodetics::Converter::get()->worldToGeodetic(world_pos); ``` (previous complex approach is still valid) | | *Unigine::GeodeticsTransformer::get()* | Changed to *Unigine::Plugins::Geodetics::Transformer::get()* |
- The IG Weather classes (*SkyMap*, *Meteo*, *Water*, etc.) have been moved to the *Weather* plugin. Due to this, the return value of *[IG::Manager::getMeteo()](../api/library/plugins/ig/api/class.managerinterface_cpp.md#getMeteo_Meteo)* has been changed to minimize manual migration.
- `ig_config.xml` has been split into two files: `ig_config.xml` and `weather_config.xml` - this is covered by automatic migration.
- File location of the IG content has been changed: previously the `ig_data/ig.umount` file, now it is stored as `data/modules/ig.ung` and `data/modules/weather.ung` - this is covered by automatic migration.


## Breaking Changes


### Removed Save() and Restore()


The methods ***save()*** and ***restore()*** have been removed from ***AppWorldLogic***, similarly ***saveState()*** and ***restoreState()*** have been removed from *[*Unigine::Plugin*](../api/library/common/class.plugin_cpp.md)* class. When migrating your project to 2.21, you need to manually remove these methods, otherwise your project will not compile.


## AsyncQueue Class


The *ASYNC_THREAD* enum values have been completely reordered. The *ASYNC_PRIORITY* enum has been expanded from 3 to 8 priority levels. Thread-checking methods have been renamed with a *Pool* prefix for consistency.


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***ASYNC_THREAD_ASYNC_FRAME_POOL*** | Removed. |
| ***ASYNC_PRIORITY_DEFAULT*** | Removed. Use *[**ASYNC_PRIORITY_NORMAL**](../api/library/filesystem/class.asyncqueue_cpp.md#ASYNC_PRIORITY_NORMAL)* instead. |
| ***isGPUStreamThread**( )* | Renamed. Use *[**isPoolGPUStreamThread**( )](../api/library/filesystem/class.asyncqueue_cpp.md#isPoolGPUStreamThread_bool)* instead. |
| ***isFileStreamThread**( )* | Renamed. Use *[**isPoolFileStreamThread**( )](../api/library/filesystem/class.asyncqueue_cpp.md#isPoolFileStreamThread_bool)* instead. |
| ***isAsyncThread**( )* | Renamed. Use *[**isPoolAsyncThread**( )](../api/library/filesystem/class.asyncqueue_cpp.md#isPoolAsyncThread_bool)* instead. |
| ***isBackgroundThread**( )* | Renamed. Use *[**isPoolBackgroundThread**( )](../api/library/filesystem/class.asyncqueue_cpp.md#isPoolBackgroundThread_bool)* instead. |
| ***isAsyncRenderThread**( )* | Renamed. Use *[**isPoolRenderFlushThread**( )](../api/library/filesystem/class.asyncqueue_cpp.md#isPoolRenderFlushThread_bool)* instead. |
| ***isPoolCPUShaderThread**( )* | Removed. |


#### New Functions


- *[ASYNC_THREAD_SYNC](../api/library/filesystem/class.asyncqueue_cpp.md#ASYNC_THREAD_SYNC)*
- *[ASYNC_THREAD_COMMON](../api/library/filesystem/class.asyncqueue_cpp.md#ASYNC_THREAD_COMMON)*
- *[ASYNC_THREAD_CRITICAL](../api/library/filesystem/class.asyncqueue_cpp.md#ASYNC_THREAD_CRITICAL)*
- *[ASYNC_PRIORITY_HIGHEST](../api/library/filesystem/class.asyncqueue_cpp.md#ASYNC_PRIORITY_HIGHEST)*
- *[ASYNC_PRIORITY_ABOVENORMAL](../api/library/filesystem/class.asyncqueue_cpp.md#ASYNC_PRIORITY_ABOVENORMAL)*
- *[ASYNC_PRIORITY_NORMAL](../api/library/filesystem/class.asyncqueue_cpp.md#ASYNC_PRIORITY_NORMAL)*
- *[ASYNC_PRIORITY_BELOWNORMAL](../api/library/filesystem/class.asyncqueue_cpp.md#ASYNC_PRIORITY_BELOWNORMAL)*
- *[ASYNC_PRIORITY_LOWEST](../api/library/filesystem/class.asyncqueue_cpp.md#ASYNC_PRIORITY_LOWEST)*
- *[ASYNC_PRIORITY_IDLE](../api/library/filesystem/class.asyncqueue_cpp.md#ASYNC_PRIORITY_IDLE)*
- *[**isPoolSyncThread**( )](../api/library/filesystem/class.asyncqueue_cpp.md#isPoolSyncThread_bool)*
- *[**isPoolCommonThread**( )](../api/library/filesystem/class.asyncqueue_cpp.md#isPoolCommonThread_bool)*
- *[**isPoolCriticalThread**( )](../api/library/filesystem/class.asyncqueue_cpp.md#isPoolCriticalThread_bool)*
- *[**isPoolRenderFlushThread**( )](../api/library/filesystem/class.asyncqueue_cpp.md#isPoolRenderFlushThread_bool)*


## Animations Class


#### New Functions


- *[**isAnimScriptsLoaded**( )](../api/library/animations/class.animations_cpp.md#isAnimScriptsLoaded_int)*
- *[**isAnimScriptsRebuilding**( )](../api/library/animations/class.animations_cpp.md#isAnimScriptsRebuilding_int)*
- *[**isAnimScriptsSuccessBuild**( )](../api/library/animations/class.animations_cpp.md#isAnimScriptsSuccessBuild_int)*
- *[**getNumAnimScriptTypes**( )](../api/library/animations/class.animations_cpp.md#getNumAnimScriptTypes_int)*
- *[**getAnimScriptTypeName**( int )](../api/library/animations/class.animations_cpp.md#getAnimScriptTypeName_int_cstr)*
- *[**rebuildAnimScripts**( )](../api/library/animations/class.animations_cpp.md#rebuildAnimScripts_void)*
- *[**getEventCustomLibBuild**( )](../api/library/animations/class.animations_cpp.md#getEventCustomLibBuild_Event)*


## CPUShader Class


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| *[**isRunning**( )](../api/library/common/mt/class.cpushader_cpp.md#isRunning_bool)* | Return value changed. |


#### New Functions


- *[**done**( )](../api/library/common/mt/class.cpushader_cpp.md#done_void)*
- *[NUM_PRIORITY](../api/library/common/mt/class.cpushader_cpp.md#NUM_PRIORITY)*
- *[PoolType_Auto](../api/library/common/mt/class.cpushader_cpp.md#PoolType_Auto)*
- *[PoolType_Async](../api/library/common/mt/class.cpushader_cpp.md#PoolType_Async)*
- *[PoolType_Sync](../api/library/common/mt/class.cpushader_cpp.md#PoolType_Sync)*
- *[PoolType_Critical](../api/library/common/mt/class.cpushader_cpp.md#PoolType_Critical)*
- *[PoolType_Background](../api/library/common/mt/class.cpushader_cpp.md#PoolType_Background)*
- *[PoolType_RenderFlush](../api/library/common/mt/class.cpushader_cpp.md#PoolType_RenderFlush)*
- *[PoolType_FileStream](../api/library/common/mt/class.cpushader_cpp.md#PoolType_FileStream)*
- *[PoolType_GPUStream](../api/library/common/mt/class.cpushader_cpp.md#PoolType_GPUStream)*
- *[**setFrameSync**( FrameSyncMode )](../api/library/common/mt/class.cpushader_cpp.md#setFrameSync_FrameSyncMode_void)*
- *[**getFrameSync**( )](../api/library/common/mt/class.cpushader_cpp.md#getFrameSync_FrameSyncMode)*
- *[**setPriority**( Priority )](../api/library/common/mt/class.cpushader_cpp.md#setPriority_Priority_void)*
- *[**getPriority**( )](../api/library/common/mt/class.cpushader_cpp.md#getPriority_Priority)*
- *[**setPool**( PoolType )](../api/library/common/mt/class.cpushader_cpp.md#setPool_PoolType_void)*
- *[**getPool**( )](../api/library/common/mt/class.cpushader_cpp.md#getPool_CPUShaderPoolType)*
- *[**isAutoDestroy**( )](../api/library/common/mt/class.cpushader_cpp.md#isAutoDestroy_bool)*


## CPUShaderCallableStateless Class


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| *[**CPUShaderCallableStateless**( Process, PoolType, Priority, FrameSyncMode )](../api/library/common/mt/class.cpushadercallablestateless_cpp.md#CPUShaderCallableStateless_Process_PoolType_Priority_FrameSyncMode_WaitMode)* | Set of arguments changed. |


## EditorLogic Class


In previous SDK versions callbacks were only triggered for [non-hidden](../code/formats/property_format.md#property_hidden) properties, starting from 2.21 callbacks are triggered for *hidden* ones as well.


## Ffp Class


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***TEXTURE_SAMPLE_SHADOW*** | Removed. |


## FileSystem Class


#### New Functions


- *[**getPackagesVirtualPaths**( Vector<String> & )](../api/library/filesystem/class.filesystem_cpp.md#getPackagesVirtualPaths_VECString_void)*
- *[**isPackageLoaded**( const char * )](../api/library/filesystem/class.filesystem_cpp.md#isPackageLoaded_cstr_bool)*


## Gui Class


#### New Functions


- *[**getFontFallback**( const char *, Vector<String> & )](../api/library/gui/class.gui_cpp.md#getFontFallback_cstr_VECString_void)*
- *[**setFontFallback**( const char *, const Vector<String> & )](../api/library/gui/class.gui_cpp.md#setFontFallback_cstr_VECString_void)*
- *[**getGlobalFontFallback**( Vector<String> & )](../api/library/gui/class.gui_cpp.md#getGlobalFontFallback_VECString_void)*
- *[**setGlobalFontFallback**( const Vector<String> & )](../api/library/gui/class.gui_cpp.md#setGlobalFontFallback_VECString_void)*


## ImportAnimation Class


The *ImportAnimation* class now supports a *[Skeleton](../api/library/common/import/class.importskeleton_cpp.md)* reference, linking imported animations with their skeleton data.


#### New Properties


- *[**Skeleton**](../api/library/common/import/class.importanimation_cpp.md#setSkeleton_ImportSkeleton_void)*


## ImportMesh Class


The *ImportMesh* class has been simplified. Animation-related properties (*AnimationFilepath*, *HasAnimations*) have been moved to the new *[ImportMeshSkinned](../api/library/common/import/class.importmeshskinned_cpp.md)* class. *ImportMesh* now represents only static mesh data.


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***setAnimationFilepath**( const char * )* / ***getAnimationFilepath**( )* | Moved to *[**ImportMeshSkinned**](../api/library/common/import/class.importmeshskinned_cpp.md)*. |
| ***setHasAnimations**( bool )* / ***isHasAnimations**( )* | Removed. Use *[**ImportMeshSkinned**](../api/library/common/import/class.importmeshskinned_cpp.md)* for skinned mesh data. |


## ImportNode Class


The *ImportNode* class now supports a *[MeshSkinned](../api/library/common/import/class.importmeshskinned_cpp.md)* reference, separating skinned and static mesh data during import.


#### New Properties


- *[**MeshSkinned**](../api/library/common/import/class.importnode_cpp.md#setMeshSkinned_ImportMeshSkinned_void)*


## ImportProcessor Class


The *ImportProcessor* class has been updated to support the new skeletal animation pipeline. Animation processing methods now use *[MeshSkinnedAnimation](../api/library/rendering/class.meshskinnedanimation_cpp.md)* and *[ImportMeshSkinned](../api/library/common/import/class.importmeshskinned_cpp.md)* instead of *MeshAnimation* and *ImportMesh*. New methods have been added for processing skinned meshes and skeletons.


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***processAnimation**( const Ptr<MeshAnimation> &, const Ptr<ImportAnimation> & )* | Signature changed: *[**processAnimation**( const Ptr<MeshSkinnedAnimation> &, const Ptr<ImportAnimation> & )](../api/library/common/import/class.importprocessor_cpp.md#processAnimation_MeshSkinnedAnimation_ImportAnimation_bool)*. |
| ***processAnimation**( const Ptr<MeshAnimation> &, const Ptr<ImportMesh> &, const Ptr<ImportAnimation> & )* | Signature changed: *[**processAnimation**( const Ptr<MeshSkinnedAnimation> &, const Ptr<ImportMeshSkinned> &, const Ptr<ImportAnimation> & )](../api/library/common/import/class.importprocessor_cpp.md#processAnimation_MeshSkinnedAnimation_ImportMeshSkinned_ImportAnimation_bool)*. |
| ***onProcessAnimation**( const Ptr<MeshAnimation> &, const Ptr<ImportAnimation> & )* | Signature changed: ***onProcessAnimation**( const Ptr<MeshSkinnedAnimation> &, const Ptr<ImportAnimation> & )*. |
| ***onProcessAnimation**( const Ptr<MeshAnimation> &, const Ptr<ImportMesh> &, const Ptr<ImportAnimation> & )* | Signature changed: ***onProcessAnimation**( const Ptr<MeshSkinnedAnimation> &, const Ptr<ImportMeshSkinned> &, const Ptr<ImportAnimation> & )*. |


#### New Functions


- *[**processMeshSkinned**( const Ptr<MeshSkinned> &, const Ptr<ImportMeshSkinned> & )](../api/library/common/import/class.importprocessor_cpp.md#processMeshSkinned_MeshSkinned_ImportMeshSkinned_bool)*
- ***onProcessMeshSkinned**( const Ptr<MeshSkinned> &, const Ptr<ImportMeshSkinned> & )*
- *[**processSkeleton**( const Ptr<Skeleton> &, const Ptr<ImportSkeleton> & )](../api/library/common/import/class.importprocessor_cpp.md#processSkeleton_Skeleton_ImportSkeleton_bool)*
- ***onProcessSkeleton**( const Ptr<Skeleton> &, const Ptr<ImportSkeleton> & )*


## ImportScene Class


The *ImportScene* class now supports *[ImportMeshSkinned](../api/library/common/import/class.importmeshskinned_cpp.md)* and *[ImportSkeleton](../api/library/common/import/class.importskeleton_cpp.md)* objects as separate entities, enabling proper handling of skinned meshes and skeletons during import.


#### New Functions


- *[**getNumMeshSkinneds**( )](../api/library/common/import/class.importscene_cpp.md#getNumMeshSkinneds_int)*
- *[**getMeshSkinned**( int )](../api/library/common/import/class.importscene_cpp.md#getMeshSkinned_int_ImportMeshSkinned)*
- *[**addMeshSkinned**( const Ptr<ImportNode> & )](../api/library/common/import/class.importscene_cpp.md#addMeshSkinned_ImportNode_ImportMeshSkinned)*
- *[**removeMeshSkinned**( const Ptr<ImportMeshSkinned> & )](../api/library/common/import/class.importscene_cpp.md#removeMeshSkinned_ImportMeshSkinned_void)*
- *[**getNumSkeletons**( )](../api/library/common/import/class.importscene_cpp.md#getNumSkeletons_int)*
- *[**getSkeleton**( int )](../api/library/common/import/class.importscene_cpp.md#getSkeleton_int_ImportSkeleton)*
- *[**addSkeleton**( )](../api/library/common/import/class.importscene_cpp.md#addSkeleton_ImportSkeleton)*
- *[**removeSkeleton**( const Ptr<ImportSkeleton> & )](../api/library/common/import/class.importscene_cpp.md#removeSkeleton_ImportSkeleton_void)*


## Importer Class


The *Importer* class has been updated for the new skeletal animation pipeline. The *IMPORT_JOINTS* flag has been renamed as *IMPORT_SKELETONS*. Animation import methods now use *[MeshSkinnedAnimation](../api/library/rendering/class.meshskinnedanimation_cpp.md)* and *[ImportMeshSkinned](../api/library/common/import/class.importmeshskinned_cpp.md)* instead of *MeshAnimation* and *ImportMesh*. New methods and processors have been added for importing skinned meshes and skeletons.


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***IMPORT_JOINTS*** | Renamed as *[**IMPORT_SKELETONS**](../api/library/common/import/class.importer_cpp.md#IMPORT_SKELETONS)*. |
| ***importAnimation**( const Ptr<ImportProcessor> &, const Ptr<MeshAnimation> &, const Ptr<ImportAnimation> & )* | Signature changed: *[**importAnimation**( const Ptr<ImportProcessor> &, const Ptr<MeshSkinnedAnimation> &, const Ptr<ImportAnimation> & )](../api/library/common/import/class.importer_cpp.md#importAnimation_ImportProcessor_MeshSkinnedAnimation_ImportAnimation_bool)*. |
| ***importAnimation**( const Ptr<ImportProcessor> &, const Ptr<MeshAnimation> &, const Ptr<ImportMesh> &, const Ptr<ImportAnimation> & )* | Signature changed: *[**importAnimation**( const Ptr<ImportProcessor> &, const Ptr<MeshSkinnedAnimation> &, const Ptr<ImportMeshSkinned> &, const Ptr<ImportAnimation> & )](../api/library/common/import/class.importer_cpp.md#importAnimation_ImportProcessor_MeshSkinnedAnimation_ImportMeshSkinned_ImportAnimation_bool)*. |
| ***onImportAnimation**( const Ptr<ImportProcessor> &, const Ptr<MeshAnimation> &, const Ptr<ImportAnimation> & )* | Signature changed: ***onImportAnimation**( const Ptr<ImportProcessor> &, const Ptr<MeshSkinnedAnimation> &, const Ptr<ImportAnimation> & )*. |
| ***onImportAnimation**( const Ptr<ImportProcessor> &, const Ptr<MeshAnimation> &, const Ptr<ImportMesh> &, const Ptr<ImportAnimation> & )* | Signature changed: ***onImportAnimation**( const Ptr<ImportProcessor> &, const Ptr<MeshSkinnedAnimation> &, const Ptr<ImportMeshSkinned> &, const Ptr<ImportAnimation> & )*. |
| ***checkSupportedAnimation**( const Ptr<ImportMesh> &, const Ptr<ImportAnimation> & )* | Signature changed: *[**checkSupportedAnimation**( const Ptr<ImportMeshSkinned> &, const Ptr<ImportAnimation> & )](../api/library/common/import/class.importer_cpp.md#checkSupportedAnimation_ImportMeshSkinned_ImportAnimation_bool)*. |
| ***checkDefaultAnimation**( const Ptr<ImportMesh> &, const Ptr<ImportAnimation> & )* | Signature changed: *[**checkDefaultAnimation**( const Ptr<ImportMeshSkinned> &, const Ptr<ImportAnimation> & )](../api/library/common/import/class.importer_cpp.md#checkDefaultAnimation_ImportMeshSkinned_ImportAnimation_bool)*. |
| ***onCheckSupportedAnimation**( const Ptr<ImportMesh> &, const Ptr<ImportAnimation> & )* | Signature changed: ***onCheckSupportedAnimation**( const Ptr<ImportMeshSkinned> &, const Ptr<ImportAnimation> & )*. |
| ***onCheckDefaultAnimation**( const Ptr<ImportMesh> &, const Ptr<ImportAnimation> & )* | Signature changed: ***onCheckDefaultAnimation**( const Ptr<ImportMeshSkinned> &, const Ptr<ImportAnimation> & )*. |


#### New Properties


- *[**MeshSkinnedsProcessor**](../api/library/common/import/class.importer_cpp.md#setMeshSkinnedsProcessor_cstr_void)*
- *[**SkeletonsProcessor**](../api/library/common/import/class.importer_cpp.md#setSkeletonsProcessor_cstr_void)*


#### New Functions


- *[**importMeshSkinned**( const Ptr<ImportProcessor> &, const Ptr<MeshSkinned> &, const Ptr<ImportMeshSkinned> & )](../api/library/common/import/class.importer_cpp.md#importMeshSkinned_ImportProcessor_MeshSkinned_ImportMeshSkinned_bool)*
- *[**importSkeleton**( const Ptr<ImportProcessor> &, const Ptr<Skeleton> &, const Ptr<ImportSkeleton> & )](../api/library/common/import/class.importer_cpp.md#importSkeleton_ImportProcessor_Skeleton_ImportSkeleton_bool)*
- ***onImportMeshSkinned**( const Ptr<ImportProcessor> &, const Ptr<MeshSkinned> &, const Ptr<ImportMeshSkinned> & )*
- ***onImportSkeleton**( const Ptr<ImportProcessor> &, const Ptr<Skeleton> &, const Ptr<ImportSkeleton> & )*


## Material Class


#### New Functions


- *[TEXTURE_SOURCE_REFLECTION_SKY](../api/library/rendering/class.material_cpp.md#TEXTURE_SOURCE_REFLECTION_SKY)*
- *[TEXTURE_SOURCE_REFLECTION_VOXEL_PROBE](../api/library/rendering/class.material_cpp.md#TEXTURE_SOURCE_REFLECTION_VOXEL_PROBE)*
- *[TEXTURE_SOURCE_REFLECTION_ENV_PROBE](../api/library/rendering/class.material_cpp.md#TEXTURE_SOURCE_REFLECTION_ENV_PROBE)*


## Mesh Class


All bone-related methods have been removed - skeleton data is now managed via the *[Skeleton](../api/library/animations/skeletal/class.skeleton_cpp.md)* class. All morph target-related methods (*SurfaceTarget*, *Weight*) have been removed. The *target* parameter has been removed from vertex, normal, tangent, intersection, and surface methods.


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***setBoneName**( int, const char * )* | Removed. |
| ***getBoneName**( int )* | Removed. |
| ***setBoneParent**( int, int )* | Removed. |
| ***getBoneParent**( int )* | Removed. |
| ***setBoneTransform**( int, const Math::mat4 & )* | Removed. |
| ***getBoneTransform**( int )* | Removed. |
| ***setBoneTransforms**( const Vector<Math::mat4> & )* | Removed. |
| ***getBoneTransforms**( Vector<Math::mat4> & )* | Removed. |
| ***getNumBones**( )* | Removed. |
| ***setNumSurfaceTargets**( int, int )* | Removed. |
| ***getNumSurfaceTargets**( int )* | Removed. |
| ***setNumWeights**( int, int )* | Removed. |
| ***getNumWeights**( int )* | Removed. |
| ***setSurfaceTargetName**( int, int, const char * )* | Removed. |
| ***getSurfaceTargetName**( int, int )* | Removed. |
| ***setWeightBones**( int, const Math::ivec4 &, int )* | Removed. |
| ***getWeightBones**( int, int )* | Removed. |
| ***setWeightCount**( int, int, int )* | Removed. |
| ***getWeightCount**( int, int )* | Removed. |
| ***setWeightWeights**( int, const Math::vec4 &, int )* | Removed. |
| ***getWeightWeights**( int, int )* | Removed. |
| ***addBone**( const char *, int )* | Removed. |
| ***addSurfaceTarget**( int, const char * )* | Removed. |
| ***findBone**( const char * )* | Removed. |
| ***findSurfaceTarget**( int, const char * )* | Removed. |
| *[**getIntersection**( const Math::dvec3 &, const Math::dvec3 &, Math::dvec3 *, Math::vec3 *, int *, int )](../api/library/rendering/class.mesh_cpp.md#getIntersection_dvec3_dvec3_dvec3_vec3_int_int_int)* | Set of arguments changed. |
| *[**getIntersection**( const Math::vec3 &, const Math::vec3 &, Math::vec3 *, Math::vec3 *, int *, int )](../api/library/rendering/class.mesh_cpp.md#getIntersection_vec3_vec3_vec3_vec3_int_int_int)* | Set of arguments changed. |
| *[**setNormal**( int, const Math::vec3 &, int )](../api/library/rendering/class.mesh_cpp.md#setNormal_int_vec3_int_void)* | Set of arguments changed. |
| *[**getNormal**( int, int )](../api/library/rendering/class.mesh_cpp.md#getNormal_int_int_vec3)* | Set of arguments changed. |
| *[**setNumNormals**( int, int )](../api/library/rendering/class.mesh_cpp.md#setNumNormals_int_int_void)* | Set of arguments changed. |
| *[**getNumNormals**( int )](../api/library/rendering/class.mesh_cpp.md#getNumNormals_int_int)* | Set of arguments changed. |
| *[**setNumTangents**( int, int )](../api/library/rendering/class.mesh_cpp.md#setNumTangents_int_int_void)* | Set of arguments changed. |
| *[**getNumTangents**( int )](../api/library/rendering/class.mesh_cpp.md#getNumTangents_int_int)* | Set of arguments changed. |
| *[**setNumVertex**( int, int )](../api/library/rendering/class.mesh_cpp.md#setNumVertex_int_int_void)* | Set of arguments changed. |
| *[**getNumVertex**( int )](../api/library/rendering/class.mesh_cpp.md#getNumVertex_int_int)* | Set of arguments changed. |
| *[**setSurfaceTransform**( const Math::mat4 &, int )](../api/library/rendering/class.mesh_cpp.md#setSurfaceTransform_mat4_int_int)* | Set of arguments changed. |
| *[**setTangent**( int, const Math::quat &, int )](../api/library/rendering/class.mesh_cpp.md#setTangent_int_quat_int_void)* | Set of arguments changed. |
| *[**getTangent**( int, int )](../api/library/rendering/class.mesh_cpp.md#getTangent_int_int_quat)* | Set of arguments changed. |
| *[**setVertex**( int, const Math::vec3 &, int )](../api/library/rendering/class.mesh_cpp.md#setVertex_int_vec3_int_void)* | Set of arguments changed. |
| *[**getVertex**( int, int )](../api/library/rendering/class.mesh_cpp.md#getVertex_int_int_vec3)* | Set of arguments changed. |
| *[**addMeshSurface**( int, const Ptr<ConstMesh> &, int, int )](../api/library/rendering/class.mesh_cpp.md#addMeshSurface_int_ConstMesh_int_int_int)* | Set of arguments changed. |
| *[**addMeshSurface**( const char *, const Ptr<ConstMesh> &, int, int )](../api/library/rendering/class.mesh_cpp.md#addMeshSurface_cstr_ConstMesh_int_int_int)* | Set of arguments changed. |
| *[**addNormal**( const Math::vec3 &, int )](../api/library/rendering/class.mesh_cpp.md#addNormal_vec3_int_void)* | Set of arguments changed. |
| *[**addTangent**( const Math::quat &, int )](../api/library/rendering/class.mesh_cpp.md#addTangent_quat_int_void)* | Set of arguments changed. |
| *[**addVertex**( const Math::vec3 &, int )](../api/library/rendering/class.mesh_cpp.md#addVertex_vec3_int_void)* | Set of arguments changed. |
| *[**addVertex**( const Vector<Math::vec3> &, int )](../api/library/rendering/class.mesh_cpp.md#addVertex_VECvec3_int_void)* | Set of arguments changed. |
| *[**createNormals**( int )](../api/library/rendering/class.mesh_cpp.md#createNormals_int_int)* | Set of arguments changed. |
| *[**createNormals**( float, int )](../api/library/rendering/class.mesh_cpp.md#createNormals_float_int_int)* | Set of arguments changed. |
| *[**createTangents**( int )](../api/library/rendering/class.mesh_cpp.md#createTangents_int_int)* | Set of arguments changed. |
| *[**addNormals**( const Vector<Math::vec3> &, int )](../api/library/rendering/class.mesh_cpp.md#addNormals_VECvec3_int_void)* | Set of arguments changed. |
| *[**addTangents**( const Vector<Math::quat> &, int )](../api/library/rendering/class.mesh_cpp.md#addTangents_VECquat_int_void)* | Set of arguments changed. |
| *[**getVertices**( int )](../api/library/rendering/class.mesh_cpp.md#getVertices_int_VECvec3)* | Set of arguments changed. |
| *[**getNormals**( int )](../api/library/rendering/class.mesh_cpp.md#getNormals_int_VECvec3)* | Set of arguments changed. |
| *[**getTangents**( int )](../api/library/rendering/class.mesh_cpp.md#getTangents_int_VECquat)* | Set of arguments changed. |
| *[**clearSurface**( int )](../api/library/rendering/class.mesh_cpp.md#clearSurface_int_void)* | Set of arguments changed. |


## MeshAnimation Class


The *MeshAnimation* class has been renamed as *[MeshSkinnedAnimation](../api/library/rendering/class.meshskinnedanimation_cpp.md)*. The API has been reworked: bone-based methods have been replaced with joint-based methods, and the class now references a shared *[Skeleton](../api/library/animations/skeletal/class.skeleton_cpp.md)*.


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| Class **MeshAnimation** | Renamed as *[**MeshSkinnedAnimation**](../api/library/rendering/class.meshskinnedanimation_cpp.md)*. |
| ***getNumBones**( )* | Replaced with *[**getNumSrcJoints**( )](../api/library/rendering/class.meshskinnedanimation_cpp.md#getNumSrcJoints_int)*. |
| ***findBone**( const char * )* | Replaced with *[**findSrcJoint**( const char * )](../api/library/rendering/class.meshskinnedanimation_cpp.md#findSrcJoint_cstr_int)*. |
| ***addBone**( const char *, int )* | Removed. Skeleton data is now managed via *[Skeleton](../api/library/animations/skeletal/class.skeleton_cpp.md)*. |
| ***setBoneName**( int, const char * )* | Removed. Use *[**getSrcJointName**( int )](../api/library/rendering/class.meshskinnedanimation_cpp.md#getSrcJointName_int_cstr)* (read-only). |
| ***getBoneName**( int )* | Replaced with *[**getSrcJointName**( int )](../api/library/rendering/class.meshskinnedanimation_cpp.md#getSrcJointName_int_cstr)*. |
| ***setBoneParent**( int, int )* | Removed. Use *[**getSrcJointParent**( int )](../api/library/rendering/class.meshskinnedanimation_cpp.md#getSrcJointParent_int_int)* (read-only). |
| ***getBoneParent**( int )* | Replaced with *[**getSrcJointParent**( int )](../api/library/rendering/class.meshskinnedanimation_cpp.md#getSrcJointParent_int_int)*. |
| ***setBoneTransform**( int, const Math::mat4 & )* | Removed. Use frame-based methods. |
| ***getBoneTransform**( int )* | Removed. Use frame-based methods. |
| ***getNumAnimationBones**( )* | Replaced with *[**getNumAnimatedJoints**( )](../api/library/rendering/class.meshskinnedanimation_cpp.md#getNumAnimatedJoints_int)*. |


## Node Class


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***WORLD_TRANSFORM_BONE*** | Renamed as *[**WORLD_TRANSFORM_JOINT**](../api/library/nodes/class.node_cpp.md#WORLD_TRANSFORM_JOINT)*. |


#### New Functions


- *[NODE_SKELETON_POSE](../api/library/nodes/class.node_cpp.md#NODE_SKELETON_POSE)*
- *[OBJECT_MESH_SKINNED_LEGACY](../api/library/nodes/class.node_cpp.md#OBJECT_MESH_SKINNED_LEGACY)*


## ObjectMeshSkinned Class


The *ObjectMeshSkinned* class has been completely reworked. The previous class (with animation layers, bone transforms, IK chains, look-at chains, constraints, retargeting, and animation playback) has been renamed as *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cpp.md)*. A new simplified *[ObjectMeshSkinned](../api/library/objects/class.objectmeshskinned_cpp.md)* class has been created, which provides only mesh data access, joint transforms, and morph targets. If your code uses any of the removed functionality, switch to *ObjectMeshSkinnedLegacy*.


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***getMesh**( Ptr<Mesh> & )* | Set of arguments changed: *[**getMesh**( Ptr<MeshSkinned> & )](../api/library/objects/class.objectmeshskinned_cpp.md#getMesh_MeshSkinned_int)*. |
| ***applyMeshProcedural**( const Ptr<ConstMesh> & )* | Set of arguments changed: *[**applyMeshProcedural**( const Ptr<ConstMeshSkinned> & )](../api/library/objects/class.objectmeshskinned_cpp.md#applyMeshProcedural_ConstMeshSkinned_int)*. |
| All animation playback methods (**play**, **stop**, **isPlaying**, **isStopped**, **setControlled**, **setLoop**, **setTime**, **setSpeed**, **setAnimPath**, **setInterpolationAccuracy**, etc.) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cpp.md)*. |
| All layer methods (**addLayer**, **removeLayer**, **setLayerEnabled**, **setLayerWeight**, **copyLayer**, **lerpLayer**, **mulLayer**, **setLayerBoneTransform**, **setLayerFrame**, **setLayerAnimationFilePath**, etc.) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cpp.md)*. |
| All bone methods (**getNumBones**, **getBoneName**, **findBone**, **getBoneParent**, **setBoneTransform**, **getBoneSkinningTransform**, **getBoneBindLocalTransform**, **copyBoneTransforms**, etc.) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cpp.md)*. |
| All retargeting methods (**setRetargeting**, **removeRetargeting**, **getRetargeting**, **isRetargeting**) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cpp.md)*. |
| All IK chain methods (**addIKChain**, **setIKChainEnabled**, **setIKChainTargetPosition**, etc.) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cpp.md)*. |
| All look-at chain methods (**addLookAtChain**, **setLookAtChainEnabled**, **setLookAtChainTargetPosition**, etc.) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cpp.md)*. |
| All bone constraint methods (**addBoneConstraint**, **setBoneConstraintEnabled**, **setBoneConstraintYawAngles**, etc.) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cpp.md)*. |
| All bind node methods (**setBindNode**, **getBindNode**, **setBindNodeSpace**, **setBindMode**, etc.) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cpp.md)*. |
| All visualization methods (**setVisualizeAllBones**, **addVisualizeBone**, **addVisualizeIKChain**, **addVisualizeLookAtChain**, etc.) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cpp.md)*. |
| All events (**getEventUpdate**, **getEventBeginLookAtSolvers**, **getEventEndLookAtSolvers**, **getEventBeginIKSolvers**, **getEventEndIKSolvers**, **getEventBeginBoneConstraints**, **getEventEndBoneConstraints**) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cpp.md)*. |
| All enums (**BIND_MODE**, **NODE_SPACE**, **BONE_SPACE**, **ANIM_FRAME_USES**, **INTERPOLATION_ACCURACY**, **CHAIN_CONSTRAINT**) | Moved to *[ObjectMeshSkinnedLegacy](../api/library/objects/class.objectmeshskinnedlegacy_cpp.md)*. |


#### New Functions


- *[**getNumJoints**( )](../api/library/objects/class.objectmeshskinned_cpp.md#getNumJoints_int)*
- *[**getJointRestLocalTransform**( int )](../api/library/objects/class.objectmeshskinned_cpp.md#getJointRestLocalTransform_int_mat4)*
- *[**getJointSkinningTransform**( int )](../api/library/objects/class.objectmeshskinned_cpp.md#getJointSkinningTransform_int_mat4)*
- *[**getSurfaceName**( int )](../api/library/objects/class.objectmeshskinned_cpp.md#getSurfaceName_int_cstr)*
- *[**findSurface**( const char * )](../api/library/objects/class.objectmeshskinned_cpp.md#findSurface_cstr_int)*


## PoolCPUShaders Class


The *PoolCPUShaders* class has been completely removed from the API. Thread pools are now managed by the *[ThreadsPool](../api/library/common/mt/class.threadspool_cpp.md)* class. For details on the engine's threading model, see the [Thread System in UNIGINE](../code/fundamentals/thread_system/index.md) article.


## Profiler Class


#### New Functions


- *[**getEventProfileDumpEnd( )**](../api/library/engine/class.profiler_cpp.md#getEventProfileDumpEnd_Event)*
- *[**getEventProfileDumpStart( )**](../api/library/engine/class.profiler_cpp.md#getEventProfileDumpStart_Event)*
- *[**startProfilerDump**( float, const char * )](../api/library/engine/class.profiler_cpp.md#startProfilerDump_float_cstr_void)*
- *[**startProfilerDump**( int, const char * )](../api/library/engine/class.profiler_cpp.md#startProfilerDump_int_cstr_void)*
- *[**startProfilerDump**( const char * )](../api/library/engine/class.profiler_cpp.md#startProfilerDump_cstr_void)*
- *[**isProfilerDumpEnabled**( )](../api/library/engine/class.profiler_cpp.md#isProfilerDumpEnabled_int)*
- *[**stopProfilerDump**( )](../api/library/engine/class.profiler_cpp.md#stopProfilerDump_void)*


## Render Class


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| *[**memoryClear**( bool )](../api/library/rendering/class.render_cpp.md#memoryClear_int_void)* | Set of arguments changed. |
| ***setTransparentMultipleEnvProbes( bool )*** | Removed. |
| ***isTransparentMultipleEnvProbes( )*** | Removed. |
| ***setTransparentLight( bool )*** | Removed. |
| ***isTransparentLight()*** | Removed. |
| ***setTransparentAmbient( bool )*** | Removed. |
| ***isTransparentAmbient()*** | Removed. |
| ***setLightsTileGridSize( int )*** | Removed. |
| ***getLightsTileGridSize()*** | Removed. |
| ***setLightsMaxPerBatch( int )*** | Removed. |
| ***getLightsMaxPerBatch()*** | Removed. |
| ***setSSSSSTAAMaxFramesByVelocity( float )*** | Removed. |
| ***getSSSSSTAAMaxFramesByVelocity()*** | Removed. |
| ***setSSSSSTAAMinFramesByVelocity( float )*** | Removed. |
| ***getSSSSSTAAMinFramesByVelocity()*** | Removed. |
| ***setTAAMaxFramesByVelocity( float )*** | Removed. |
| ***getTAAMaxFramesByVelocity()*** | Removed. |
| ***setTAAMinFramesByVelocity( float )*** | Removed. |
| ***getTAAMinFramesByVelocity()*** | Removed. |
| ***setTAAInformationLostFrameCount( int )*** | Removed. |
| ***getTAAInformationLostFrameCount()*** | Removed. |
| ***setFSRAutoReactiveEnabled( bool )*** | Removed. |
| ***isFSRAutoReactiveEnabled()*** | Removed. |
| ***setFSRAutoReactiveScale( float )*** | Removed. |
| ***getFSRAutoReactiveScale()*** | Removed. |
| ***setFSRAutoReactiveMax( float )*** | Removed. |
| ***getFSRAutoReactiveMax()*** | Removed. |
| ***setFSRAutoTCScale( float )*** | Removed. |
| ***getFSRAutoTCScale()*** | Removed. |
| ***setFSRAutoTCThreshold( float )*** | Removed. |
| ***getFSRAutoTCThreshold()*** | Removed. |
| ***setUpscalePost( bool )*** | Removed. |
| ***isUpscalePost()*** | Removed. |


#### New Functions


- *[RENDER_FSR_MODE_NATIVE_AA](../api/library/rendering/class.render_cpp.md#RENDER_FSR_MODE_NATIVE_AA)*
- *[RENDER_FSR_MODE_CUSTOM](../api/library/rendering/class.render_cpp.md#RENDER_FSR_MODE_CUSTOM)*
- *[SHADING_QUALITY_LOW](../api/library/rendering/class.render_cpp.md#SHADING_QUALITY_LOW)*
- *[SHADING_QUALITY_MEDIUM](../api/library/rendering/class.render_cpp.md#SHADING_QUALITY_MEDIUM)*
- *[SHADING_QUALITY_HIGH](../api/library/rendering/class.render_cpp.md#SHADING_QUALITY_HIGH)*
- *[SHOW_VERTEX_DENSITY_MODE_DISCRETE_THRESHOLD](../api/library/rendering/class.render_cpp.md#SHOW_VERTEX_DENSITY_MODE_DISCRETE_THRESHOLD)*
- *[SHOW_VERTEX_DENSITY_MODE_GRADIENT](../api/library/rendering/class.render_cpp.md#SHOW_VERTEX_DENSITY_MODE_GRADIENT)*
- *[SHOW_QUAD_OVERDRAW_DISPLAY_MODE_GRADIENT](../api/library/rendering/class.render_cpp.md#SHOW_QUAD_OVERDRAW_DISPLAY_MODE_GRADIENT)*
- *[SHOW_QUAD_OVERDRAW_DISPLAY_MODE_DISCRETE_THRESHOLD](../api/library/rendering/class.render_cpp.md#SHOW_QUAD_OVERDRAW_DISPLAY_MODE_DISCRETE_THRESHOLD)*
- *[SHOW_QUAD_OVERDRAW_PASSES_ALL](../api/library/rendering/class.render_cpp.md#SHOW_QUAD_OVERDRAW_PASSES_ALL)*
- *[SHOW_QUAD_OVERDRAW_PASSES_GEOMETRY](../api/library/rendering/class.render_cpp.md#SHOW_QUAD_OVERDRAW_PASSES_GEOMETRY)*
- *[SHOW_QUAD_OVERDRAW_PASSES_GEOMETRY_WITHOUT_DEPTH_PRE_PASS](../api/library/rendering/class.render_cpp.md#SHOW_QUAD_OVERDRAW_PASSES_GEOMETRY_WITHOUT_DEPTH_PRE_PASS)*
- *[PASS_VISUALIZER_QUAD_OVERDRAW](../api/library/rendering/class.render_cpp.md#PASS_VISUALIZER_QUAD_OVERDRAW)*
- *[PASS_VISUALIZER_QUAD_OVERDRAW_NO_DEPTH_PREPASS](../api/library/rendering/class.render_cpp.md#PASS_VISUALIZER_QUAD_OVERDRAW_NO_DEPTH_PREPASS)*
- *[STREAMING_IGPU_VRAM_MODE_SYSTEM](../api/library/rendering/class.render_cpp.md#STREAMING_IGPU_VRAM_MODE_SYSTEM)*
- *[STREAMING_IGPU_VRAM_MODE_SIZE](../api/library/rendering/class.render_cpp.md#STREAMING_IGPU_VRAM_MODE_SIZE)*
- *[STREAMING_IGPU_VRAM_MODE_BALANCE](../api/library/rendering/class.render_cpp.md#STREAMING_IGPU_VRAM_MODE_BALANCE)*
- *[RENDER_UPSCALE_ORDER_BEFORE_POST_EFFECTS](../api/library/rendering/class.render_cpp.md#RENDER_UPSCALE_ORDER_BEFORE_POST_EFFECTS)*
- *[RENDER_UPSCALE_ORDER_AFTER_ADAPTATION_COLOR](../api/library/rendering/class.render_cpp.md#RENDER_UPSCALE_ORDER_AFTER_ADAPTATION_COLOR)*
- *[RENDER_UPSCALE_ORDER_BEFORE_TAA](../api/library/rendering/class.render_cpp.md#RENDER_UPSCALE_ORDER_BEFORE_TAA)*
- *[RENDER_UPSCALE_ORDER_AFTER_POST_EFFECTS](../api/library/rendering/class.render_cpp.md#RENDER_UPSCALE_ORDER_AFTER_POST_EFFECTS)*
- *[RENDER_UPSCALE_NUM_ORDERS](../api/library/rendering/class.render_cpp.md#RENDER_UPSCALE_NUM_ORDERS)*
- *[**setEnvironmentHazeResolution**( int )](../api/library/rendering/class.render_cpp.md#setEnvironmentHazeResolution_int_void)*
- *[**getEnvironmentHazeResolution**( )](../api/library/rendering/class.render_cpp.md#getEnvironmentHazeResolution_int)*
- *[**isShowTransparentLightingLightWorld**( )](../api/library/rendering/class.render_cpp.md#isShowTransparentLightingLightWorld_int)*
- *[**setShowTransparentLightingLightWorld**( bool )](../api/library/rendering/class.render_cpp.md#setShowTransparentLightingLightWorld_int_void)*
- *[**isShowTransparentLightingLightProj**( )](../api/library/rendering/class.render_cpp.md#isShowTransparentLightingLightProj_int)*
- *[**setShowTransparentLightingLightProj**( bool )](../api/library/rendering/class.render_cpp.md#setShowTransparentLightingLightProj_int_void)*
- *[**isShowTransparentLightingLightOmni**( )](../api/library/rendering/class.render_cpp.md#isShowTransparentLightingLightOmni_int)*
- *[**setShowTransparentLightingLightOmni**( bool )](../api/library/rendering/class.render_cpp.md#setShowTransparentLightingLightOmni_int_void)*
- *[**isShowTransparentLightingPlanarProbe**( )](../api/library/rendering/class.render_cpp.md#isShowTransparentLightingPlanarProbe_int)*
- *[**setShowTransparentLightingPlanarProbe**( bool )](../api/library/rendering/class.render_cpp.md#setShowTransparentLightingPlanarProbe_int_void)*
- *[**isShowTransparentLightingVoxelProbe**( )](../api/library/rendering/class.render_cpp.md#isShowTransparentLightingVoxelProbe_int)*
- *[**setShowTransparentLightingVoxelProbe**( bool )](../api/library/rendering/class.render_cpp.md#setShowTransparentLightingVoxelProbe_int_void)*
- *[**isShowTransparentLightingEnvironmentProbe**( )](../api/library/rendering/class.render_cpp.md#isShowTransparentLightingEnvironmentProbe_int)*
- *[**setShowTransparentLightingEnvironmentProbe**( bool )](../api/library/rendering/class.render_cpp.md#setShowTransparentLightingEnvironmentProbe_int_void)*
- *[**isShowTransparentLightingAmbient**( )](../api/library/rendering/class.render_cpp.md#isShowTransparentLightingAmbient_int)*
- *[**setShowTransparentLightingAmbient**( bool )](../api/library/rendering/class.render_cpp.md#setShowTransparentLightingAmbient_int_void)*
- *[**isShowTransparentGBuffer**( )](../api/library/rendering/class.render_cpp.md#isShowTransparentGBuffer_int)*
- *[**setShowTransparentGBuffer**( bool )](../api/library/rendering/class.render_cpp.md#setShowTransparentGBuffer_int_void)*
- *[**isShowDepthPrePass**( )](../api/library/rendering/class.render_cpp.md#isShowDepthPrePass_int)*
- *[**setShowDepthPrePass**( bool )](../api/library/rendering/class.render_cpp.md#setShowDepthPrePass_int_void)*
- *[**isShowProjAndOmniShadowCasters**( )](../api/library/rendering/class.render_cpp.md#isShowProjAndOmniShadowCasters_int)*
- *[**setShowProjAndOmniShadowCasters**( bool )](../api/library/rendering/class.render_cpp.md#setShowProjAndOmniShadowCasters_int_void)*
- *[**getCloudsEnvironmentColor**( )](../api/library/rendering/class.render_cpp.md#getCloudsEnvironmentColor_vec4)*
- *[**setCloudsEnvironmentColor**( const Math::vec4 & )](../api/library/rendering/class.render_cpp.md#setCloudsEnvironmentColor_vec4_void)*
- *[**getCloudsEnvironmentSkyColor**( )](../api/library/rendering/class.render_cpp.md#getCloudsEnvironmentSkyColor_vec4)*
- *[**setCloudsEnvironmentSkyColor**( const Math::vec4 & )](../api/library/rendering/class.render_cpp.md#setCloudsEnvironmentSkyColor_vec4_void)*
- *[**isCloudsEnvironmentSky**( )](../api/library/rendering/class.render_cpp.md#isCloudsEnvironmentSky_int)*
- *[**setCloudsEnvironmentSky**( bool )](../api/library/rendering/class.render_cpp.md#setCloudsEnvironmentSky_int_void)*
- *[**getCloudsEnvironmentTexturePath**( )](../api/library/rendering/class.render_cpp.md#getCloudsEnvironmentTexturePath_cstr)*
- *[**setCloudsEnvironmentTexturePath**( const char * )](../api/library/rendering/class.render_cpp.md#setCloudsEnvironmentTexturePath_cstr_void)*
- *[**getFSRCustomResolutionScale**( )](../api/library/rendering/class.render_cpp.md#getFSRCustomResolutionScale_float)*
- *[**setFSRCustomResolutionScale**( float )](../api/library/rendering/class.render_cpp.md#setFSRCustomResolutionScale_float_void)*
- *[**isDLSSResolutionScaleEnabled**( )](../api/library/rendering/class.render_cpp.md#isDLSSResolutionScaleEnabled_int)*
- *[**setDLSSResolutionScaleEnabled**( bool )](../api/library/rendering/class.render_cpp.md#setDLSSResolutionScaleEnabled_int_void)*
- *[**getDLSSResolutionScaleValue**( )](../api/library/rendering/class.render_cpp.md#getDLSSResolutionScaleValue_float)*
- *[**setDLSSResolutionScaleValue**( float )](../api/library/rendering/class.render_cpp.md#setDLSSResolutionScaleValue_float_void)*
- *[**isUpscaleFixFlicker**( )](../api/library/rendering/class.render_cpp.md#isUpscaleFixFlicker_int)*
- *[**setUpscaleFixFlicker**( bool )](../api/library/rendering/class.render_cpp.md#setUpscaleFixFlicker_int_void)*
- *[**getOccluderDistance**( )](../api/library/rendering/class.render_cpp.md#getOccluderDistance_float)*
- *[**setOccluderDistance**( float )](../api/library/rendering/class.render_cpp.md#setOccluderDistance_float_void)*
- *[**setSharpenResolution**( int )](../api/library/rendering/class.render_cpp.md#setSharpenResolution_int_void)*
- *[**getSharpenResolution**( )](../api/library/rendering/class.render_cpp.md#getSharpenResolution_int)*
- *[**getShowQuadOverdrawBlend**( )](../api/library/rendering/class.render_cpp.md#getShowQuadOverdrawBlend_float)*
- *[**setShowQuadOverdrawBlend**( float )](../api/library/rendering/class.render_cpp.md#setShowQuadOverdrawBlend_float_void)*
- *[**getShowQuadOverdrawThreshold**( )](../api/library/rendering/class.render_cpp.md#getShowQuadOverdrawThreshold_int)*
- *[**setShowQuadOverdrawThreshold**( int )](../api/library/rendering/class.render_cpp.md#setShowQuadOverdrawThreshold_int_void)*
- *[**isShowQuadOverdrawWaterGlobal**( )](../api/library/rendering/class.render_cpp.md#isShowQuadOverdrawWaterGlobal_int)*
- *[**setShowQuadOverdrawWaterGlobal**( bool )](../api/library/rendering/class.render_cpp.md#setShowQuadOverdrawWaterGlobal_int_void)*
- *[**isShowQuadOverdrawLandscapeTerrain**( )](../api/library/rendering/class.render_cpp.md#isShowQuadOverdrawLandscapeTerrain_int)*
- *[**setShowQuadOverdrawLandscapeTerrain**( bool )](../api/library/rendering/class.render_cpp.md#setShowQuadOverdrawLandscapeTerrain_int_void)*
- *[**isShowQuadOverdrawWireframe**( )](../api/library/rendering/class.render_cpp.md#isShowQuadOverdrawWireframe_int)*
- *[**setShowQuadOverdrawWireframe**( bool )](../api/library/rendering/class.render_cpp.md#setShowQuadOverdrawWireframe_int_void)*
- *[**getShowQuadOverdrawPasses**( )](../api/library/rendering/class.render_cpp.md#getShowQuadOverdrawPasses_int)*
- *[**setShowQuadOverdrawPasses**( Render::SHOW_QUAD_OVERDRAW_PASSES )](../api/library/rendering/class.render_cpp.md#setShowQuadOverdrawPasses_int_void)*
- *[**getShowQuadOverdrawDisplayMode**( )](../api/library/rendering/class.render_cpp.md#getShowQuadOverdrawDisplayMode_int)*
- *[**setShowQuadOverdrawDisplayMode**( Render::SHOW_QUAD_OVERDRAW_DISPLAY_MODE )](../api/library/rendering/class.render_cpp.md#setShowQuadOverdrawDisplayMode_int_void)*
- *[**isShowQuadOverdrawEnabled**( )](../api/library/rendering/class.render_cpp.md#isShowQuadOverdrawEnabled_int)*
- *[**setShowQuadOverdrawEnabled**( bool )](../api/library/rendering/class.render_cpp.md#setShowQuadOverdrawEnabled_int_void)*
- *[**getShowVertexDensityBlend**( )](../api/library/rendering/class.render_cpp.md#getShowVertexDensityBlend_float)*
- *[**setShowVertexDensityBlend**( float )](../api/library/rendering/class.render_cpp.md#setShowVertexDensityBlend_float_void)*
- *[**getShowVertexDensityThreshold**( )](../api/library/rendering/class.render_cpp.md#getShowVertexDensityThreshold_int)*
- *[**setShowVertexDensityThreshold**( int )](../api/library/rendering/class.render_cpp.md#setShowVertexDensityThreshold_int_void)*
- *[**getShowVertexDensitySearchArea**( )](../api/library/rendering/class.render_cpp.md#getShowVertexDensitySearchArea_int)*
- *[**setShowVertexDensitySearchArea**( int )](../api/library/rendering/class.render_cpp.md#setShowVertexDensitySearchArea_int_void)*
- *[**isShowVertexDensityDepthTest**( )](../api/library/rendering/class.render_cpp.md#isShowVertexDensityDepthTest_int)*
- *[**setShowVertexDensityDepthTest**( bool )](../api/library/rendering/class.render_cpp.md#setShowVertexDensityDepthTest_int_void)*
- *[**getShowVertexDensityMode**( )](../api/library/rendering/class.render_cpp.md#getShowVertexDensityMode_int)*
- *[**setShowVertexDensityMode**( Render::SHOW_VERTEX_DENSITY_MODE )](../api/library/rendering/class.render_cpp.md#setShowVertexDensityMode_int_void)*
- *[**isShowVertexDensityEnabled**( )](../api/library/rendering/class.render_cpp.md#isShowVertexDensityEnabled_int)*
- *[**setShowVertexDensityEnabled**( bool )](../api/library/rendering/class.render_cpp.md#setShowVertexDensityEnabled_int_void)*
- *[**setShadingQuality**( Render::SHADING_QUALITY )](../api/library/rendering/class.render_cpp.md#setShadingQuality_int_void)*
- *[**getShadingQuality**( )](../api/library/rendering/class.render_cpp.md#getShadingQuality_int)*
- *[**getNumCompiledPSOGlobal**( )](../api/library/rendering/class.render_cpp.md#getNumCompiledPSOGlobal_int)*
- *[**setStreamingIGpuVRAMMode**( Render::STREAMING_IGPU_VRAM_MODE )](../api/library/rendering/class.render_cpp.md#setStreamingIGpuVRAMMode_int_void)*
- *[**getStreamingIGpuVRAMMode**( )](../api/library/rendering/class.render_cpp.md#getStreamingIGpuVRAMMode_int)*
- *[**setStreamingIGpuVRAMSize**( int )](../api/library/rendering/class.render_cpp.md#setStreamingIGpuVRAMSize_int_void)*
- *[**getStreamingIGpuVRAMSize**( )](../api/library/rendering/class.render_cpp.md#getStreamingIGpuVRAMSize_int)*
- *[**setStreamingIGpuVRAMBalance**( int )](../api/library/rendering/class.render_cpp.md#setStreamingIGpuVRAMBalance_int_void)*
- *[**getStreamingIGpuVRAMBalance**( )](../api/library/rendering/class.render_cpp.md#getStreamingIGpuVRAMBalance_int)*
- *[**setUpscaleOrder**( Render::RENDER_UPSCALE_ORDER )](../api/library/rendering/class.render_cpp.md#setUpscaleOrder_int_void)*
- *[**getUpscaleOrder**( )](../api/library/rendering/class.render_cpp.md#getUpscaleOrder_int)*
- *[**setFSRShowDebugView**( int )](../api/library/rendering/class.render_cpp.md#setFSRShowDebugView_int_void)*
- *[**isFSRShowDebugView**( )](../api/library/rendering/class.render_cpp.md#isFSRShowDebugView_int)*
- *[**setEnvironmentDitherScale**( float )](../api/library/rendering/class.render_cpp.md#setEnvironmentDitherScale_float_void)*
- *[**getEnvironmentDitherScale**( )](../api/library/rendering/class.render_cpp.md#getEnvironmentDitherScale_float)*
- *[**setEnvironmentHazeDitherScale**( float )](../api/library/rendering/class.render_cpp.md#setEnvironmentHazeDitherScale_float_void)*
- *[**getEnvironmentHazeDitherScale**( )](../api/library/rendering/class.render_cpp.md#getEnvironmentHazeDitherScale_float)*
- *[**getEnvironmentSunAngularSize**( )](../api/library/rendering/class.render_cpp.md#getEnvironmentSunAngularSize_float)*
- *[**getEnvironmentMoonAngularSize**( )](../api/library/rendering/class.render_cpp.md#getEnvironmentMoonAngularSize_float)*
- *[**setLightsDitherScale**( float )](../api/library/rendering/class.render_cpp.md#setLightsDitherScale_float_void)*
- *[**getLightsDitherScale**( )](../api/library/rendering/class.render_cpp.md#getLightsDitherScale_float)*
- *[**getEventBeginVisualizerQuadOverdraw**( )](../api/library/rendering/class.render_cpp.md#getEventBeginVisualizerQuadOverdraw_Event)*
- *[**getEventEndVisualizerQuadOverdraw**( )](../api/library/rendering/class.render_cpp.md#getEventEndVisualizerQuadOverdraw_Event)*
- *[**getEventGPUCrashDump**( )](../api/library/rendering/class.render_cpp.md#getEventGPUCrashDump_Event)*
- *[**setStreamingFreeSpaceRAMCommitted**( int )](../api/library/rendering/class.render_cpp.md#setStreamingFreeSpaceRAMCommitted_int_void)*
- *[**getStreamingFreeSpaceRAMCommitted**( )](../api/library/rendering/class.render_cpp.md#getStreamingFreeSpaceRAMCommitted_int)*
- *[**setMaterialReplaceFunc**( MaterialReplaceFunc )](../api/library/rendering/class.render_cpp.md#setMaterialReplaceFunc_MaterialReplaceFunc_void)*
- *[**getMaterialReplaceFunc**( )](../api/library/rendering/class.render_cpp.md#getMaterialReplaceFunc_MaterialReplaceFunc)*


## Renderer Class


#### New Functions


- *[**useDepthPrePass**( )](../api/library/rendering/class.renderer_cpp.md#useDepthPrePass_int)*


## RenderState Class


#### New Functions


- *[RENDER_MODE_POINTS](../api/library/rendering/class.renderstate_cpp.md#RENDER_MODE_POINTS)*
- *[RENDER_MODE_LINES](../api/library/rendering/class.renderstate_cpp.md#RENDER_MODE_LINES)*
- *[RENDER_MODE_TRIANGLES](../api/library/rendering/class.renderstate_cpp.md#RENDER_MODE_TRIANGLES)*
- *[RENDER_MODE_TRIANGLE_PATCHES](../api/library/rendering/class.renderstate_cpp.md#RENDER_MODE_TRIANGLE_PATCHES)*
- *[RENDER_MODE_QUAD_PATCHES](../api/library/rendering/class.renderstate_cpp.md#RENDER_MODE_QUAD_PATCHES)*
- *[NUM_RENDER_MODES](../api/library/rendering/class.renderstate_cpp.md#NUM_RENDER_MODES)*
- *[**getStructuredBuffer**( int )](../api/library/rendering/class.renderstate_cpp.md#getStructuredBuffer_int_StructuredBuffer)*
- *[**setIndexBuffer**( const Ptr<StructuredBuffer> &, int, int )](../api/library/rendering/class.renderstate_cpp.md#setIndexBuffer_StructuredBuffer_int_int_void)*
- *[**setVertexBuffer**( int, const Ptr<StructuredBuffer> &, int, int )](../api/library/rendering/class.renderstate_cpp.md#setVertexBuffer_int_StructuredBuffer_int_int_void)*
- *[**render**( RenderState::RENDER_MODE, int, int, int, int )](../api/library/rendering/class.renderstate_cpp.md#render_int_int_int_int_int_int)*
- *[**setDepthWrite**( bool )](../api/library/rendering/class.renderstate_cpp.md#setDepthWrite_int_void)*
- *[**isDepthWrite**( )](../api/library/rendering/class.renderstate_cpp.md#isDepthWrite_int)*
- *[**setConservativeRasterizationEnabled**( bool )](../api/library/rendering/class.renderstate_cpp.md#setConservativeRasterizationEnabled_int_void)*
- *[**isConservativeRasterizationEnabled**( )](../api/library/rendering/class.renderstate_cpp.md#isConservativeRasterizationEnabled_int)*


## Syncker::Manager Class


#### New Functions


- *[NETWORK](../api/library/plugins/syncker/class.syncker_manager_cpp.md#NETWORK)*
- *[LOAD_FROM_LOCAL_STORAGE](../api/library/plugins/syncker/class.syncker_manager_cpp.md#LOAD_FROM_LOCAL_STORAGE)*
- *[**getEasyblendSyncType**( )](../api/library/plugins/syncker/class.syncker_manager_cpp.md#getEasyblendSyncType_int)*
- *[**setEasyblendSyncType**( Manager::SPIDER_VISION_EASYBLEND_SYNC_TYPE )](../api/library/plugins/syncker/class.syncker_manager_cpp.md#setEasyblendSyncType_int_void)*


## SystemInfo Class


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***getMemoryFree**( )* | Renamed as *[**getRamFree**( )](../api/library/engine/class.systeminfo_cpp.md#getRamFree_llong)*. |
| ***getMemoryFreeCommitted**( )* | Renamed as *[**getRamCommittedFree**( )](../api/library/engine/class.systeminfo_cpp.md#getRamCommittedFree_llong)*. |
| ***getMemoryTotal**( )* | Renamed as *[**getRamTotal**( )](../api/library/engine/class.systeminfo_cpp.md#getRamTotal_llong)*. |
| ***getMemoryTotalCommitted**( )* | Renamed as *[**getRamCommittedTotal**( )](../api/library/engine/class.systeminfo_cpp.md#getRamCommittedTotal_llong)*. |
| ***getMemoryUsage**( )* | Renamed as *[**getRamUsage**( )](../api/library/engine/class.systeminfo_cpp.md#getRamUsage_llong)*. |
| ***getMemoryUsageCommitted**( )* | Renamed as *[**getRamCommittedUsage**( )](../api/library/engine/class.systeminfo_cpp.md#getRamCommittedUsage_llong)*. |
| ***getGPUMemoryFree**( )* | Renamed as *[**getGpuVRamFree**( )](../api/library/engine/class.systeminfo_cpp.md#getGpuVRamFree_llong)*. |
| ***getGPUMemoryLimit**( )* | Renamed as *[**getGpuVRamLimit**( )](../api/library/engine/class.systeminfo_cpp.md#getGpuVRamLimit_llong)*. |
| ***getGPUMemoryStatistics**( )* | Removed. Use *[**getMemoryStatistics**( )](../api/library/engine/class.systeminfo_cpp.md#getMemoryStatistics_MemoryStatistics)* instead. |


#### New Functions


- *[**getGpuVRamTotal**( )](../api/library/engine/class.systeminfo_cpp.md#getGpuVRamTotal_llong)*
- *[**getGpuVRamBudget**( )](../api/library/engine/class.systeminfo_cpp.md#getGpuVRamBudget_llong)*
- *[**getGpuVRamLimit**( )](../api/library/engine/class.systeminfo_cpp.md#getGpuVRamLimit_llong)*
- *[**getGpuVRamBackground**( )](../api/library/engine/class.systeminfo_cpp.md#getGpuVRamBackground_llong)*
- *[**getGpuVRamUsage**( )](../api/library/engine/class.systeminfo_cpp.md#getGpuVRamUsage_llong)*
- *[**getGpuRamBackground**( )](../api/library/engine/class.systeminfo_cpp.md#getGpuRamBackground_llong)*
- *[**getGpuRamUsage**( )](../api/library/engine/class.systeminfo_cpp.md#getGpuRamUsage_llong)*
- *[**getRamCommittedLimit**( )](../api/library/engine/class.systeminfo_cpp.md#getRamCommittedLimit_llong)*
- *[**getRamCommittedBackground**( )](../api/library/engine/class.systeminfo_cpp.md#getRamCommittedBackground_llong)*
- *[**getRamLimit**( )](../api/library/engine/class.systeminfo_cpp.md#getRamLimit_llong)*
- *[**outOfVRam**( )](../api/library/engine/class.systeminfo_cpp.md#outOfVRam_bool)*
- *[**outOfRam**( )](../api/library/engine/class.systeminfo_cpp.md#outOfRam_bool)*
- *[**outOfRamCommitted**( )](../api/library/engine/class.systeminfo_cpp.md#outOfRamCommitted_bool)*
- *[**getMemoryStatistics**( )](../api/library/engine/class.systeminfo_cpp.md#getMemoryStatistics_MemoryStatistics)*
- *[**getRamFrequency**( )](../api/library/engine/class.systeminfo_cpp.md#getRamFrequency_uint)*
- *[**getSwapSize**( )](../api/library/engine/class.systeminfo_cpp.md#getSwapSize_llong)*
- *[**getCPUName**( )](../api/library/engine/class.systeminfo_cpp.md#getCPUName_cstr)*
- *[**getGPUUuidString**( int )](../api/library/engine/class.systeminfo_cpp.md#getGPUUuidString_int_cstr)*
- *[**getProcessID**( )](../api/library/engine/class.systeminfo_cpp.md#getProcessID_int)*
- *[**getEnvironmentVariable**( const char * )](../api/library/engine/class.systeminfo_cpp.md#getEnvironmentVariable_cstr_cstr)*


## Texture Class


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***SAMPLER_SHADOW_COMPARE*** | Removed. |
| ***SAMPLER_SHADOW_MASK*** | Removed. |


## StructuredBuffer Class


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***USAGE_SHARED** = 1 << 3* | Value changed to 1 << 4. |


#### New Functions


- *[USAGE_DYNAMIC](../api/library/rendering/class.structuredbuffer_cpp.md#USAGE_DYNAMIC)*


## UlonValue Class


#### New Functions


- *[**getShort**( )](../api/library/common/class.ulonvalue_cpp.md#getShort_short)*


## VR Class


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***hasFeatureTrackingSpaceRaw**( )* | Removed. |
| ***TRACKING_SPACE_UNKNOWN*** | Replaced with ***TRACKING_SPACE_LOCAL***. |
| ***TRACKING_SPACE_SEATED*** | Replaced with ***TRACKING_SPACE_LOCAL***. |
| ***TRACKING_SPACE_STANDING*** | Replaced with ***TRACKING_SPACE_ABSOLUTE***. |


#### New Functions


- *[**setFoveatedFixedEyeCenterBias**( )](../api/library/vr/class.vr_cpp.md#setFoveatedFixedEyeCenterBias_float_void)*
- *[**getFoveatedFixedEyeCenterBias**( )](../api/library/vr/class.vr_cpp.md#getFoveatedFixedEyeCenterBias_float)*
- *[**getAbsoluteToLocalWorldTransform**( )](../api/library/vr/class.vr_cpp.md#getAbsoluteToLocalWorldTransform_Mat4)*


## ViewportData Class


#### New Functions


- *[WINDOW_MODE enumeration naming changed.](../api/library/plugins/spidervision/class.viewportdata_cpp.md#WINDOW_MODE)*
- *[**restoreBase**( const Ptr<Stream> & )](../api/library/plugins/spidervision/class.viewportdata_cpp.md#restoreBase_Stream_void)*
- *[**saveBase**( const Ptr<Stream> & )](../api/library/plugins/spidervision/class.viewportdata_cpp.md#saveBase_Stream_void)*


## WallGroupData Class


#### New Functions


- *[**setAspect**( float )](../api/library/plugins/spidervision/class.wallgroupdata_cpp.md#setAspect_float_void)*
- *[**getAspect**( )](../api/library/plugins/spidervision/class.wallgroupdata_cpp.md#getAspect_float)*
- *[**setVFov**( float )](../api/library/plugins/spidervision/class.wallgroupdata_cpp.md#setVFov_float_void)*
- *[**getVFov**( )](../api/library/plugins/spidervision/class.wallgroupdata_cpp.md#getVFov_float)*
- *[**setTransformType**( ViewportData::DISPLAY_TRANSFORM_TYPE )](../api/library/plugins/spidervision/class.wallgroupdata_cpp.md#setTransformType_int_void)*
- *[**getTransformType**( )](../api/library/plugins/spidervision/class.wallgroupdata_cpp.md#getTransformType_int)*


## WidgetVBox Class


#### New Functions


- *[**getBackgroundBlendDestFunc**( )](../api/library/gui/class.widgetvbox_cpp.md#getBackgroundBlendDestFunc_int)*
- *[**getBackgroundBlendSrcFunc**( )](../api/library/gui/class.widgetvbox_cpp.md#getBackgroundBlendSrcFunc_int)*
- *[**setBackgroundBlendFunc**( int, int )](../api/library/gui/class.widgetvbox_cpp.md#setBackgroundBlendFunc_int_int_void)*


## IG::Manager Class


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***getTerrain**( )* | Return type changed from *const ObjectTerrainGlobalPtr &* to *ObjectTerrainGlobalPtr*. |
| ***getGeodeticPivot**( )* | Return type changed from *const GeodeticPivotPtr &* to *GeodeticPivotPtr*. |
| ***getGeodeticsTransformer**( )* | Return type changed from *GeodeticsTransformer ** to *Plugins::Geodetics::Transformer **. |
| ***getGeodeticOrigin**( )* | Return type changed from *const Vec3 &* to *Vec3*. |
| ***getConverter**( )* | Return type changed from *IG::Converter* to *Geodetics::Converter*. |
| ***getMeteo**( )* | Return type changed from *IG::Meteo* to *Weather::Meteo*. |


#### New Functions


- *[**getNEDConverter**( )](../api/library/plugins/ig/api/class.managerinterface_cpp.md#getNEDConverter_NEDConverter)*


## IG::Entity Class


#### New Functions


- *[**setOwnerID**( int )](../api/library/plugins/ig/api/class.entity_cpp.md#setOwnerID_int_void)*
- *[**getOwnerID**( )](../api/library/plugins/ig/api/class.entity_cpp.md#getOwnerID_int)*
- *[**setDebugDescription**( const String & )](../api/library/plugins/ig/api/class.entity_cpp.md#setDebugDescription_String_void)*
- *[**getDebugDescription**( )](../api/library/plugins/ig/api/class.entity_cpp.md#getDebugDescription_String)*


## IG::NEDConverter Class


#### New Functions


- *[TARGET_COORDINATE_SYSTEM_NED](../api/library/plugins/ig/api/class.nedconverter_cpp.md#TARGET_COORDINATE_SYSTEM_NED)*
- *[TARGET_COORDINATE_SYSTEM_ENU](../api/library/plugins/ig/api/class.nedconverter_cpp.md#TARGET_COORDINATE_SYSTEM_ENU)*
- *[**setTargetCoordinateSystem**( TARGET_COORDINATE_SYSTEM )](../api/library/plugins/ig/api/class.nedconverter_cpp.md#setTargetCoordinateSystem_int_void)*
- *[**getTargetCoordinateSystem**( )](../api/library/plugins/ig/api/class.nedconverter_cpp.md#getTargetCoordinateSystem_int)*
- *[**ENUtoNED**( const dvec3 & )](../api/library/plugins/ig/api/class.nedconverter_cpp.md#ENUtoNED_dvec3_dvec3)*
- *[**NEDtoENU**( const dvec3 & )](../api/library/plugins/ig/api/class.nedconverter_cpp.md#NEDtoENU_dvec3_dvec3)*
- *[**TARGETtoENU**( const dvec3 & )](../api/library/plugins/ig/api/class.nedconverter_cpp.md#TARGETtoENU_dvec3_dvec3)*
- *[**ENUtoTARGET**( const dvec3 & )](../api/library/plugins/ig/api/class.nedconverter_cpp.md#ENUtoTARGET_dvec3_dvec3)*
- *[**ENUtoNED**( const vec3 & )](../api/library/plugins/ig/api/class.nedconverter_cpp.md#ENUtoNED_vec3_vec3)*
- *[**NEDtoENU**( const vec3 & )](../api/library/plugins/ig/api/class.nedconverter_cpp.md#NEDtoENU_vec3_vec3)*
- *[**TARGETtoENU**( const vec3 & )](../api/library/plugins/ig/api/class.nedconverter_cpp.md#TARGETtoENU_vec3_vec3)*
- *[**ENUtoTARGET**( const vec3 & )](../api/library/plugins/ig/api/class.nedconverter_cpp.md#ENUtoTARGET_vec3_vec3)*
- *[**eulerENUToRotation**( const vec3 & )](../api/library/plugins/ig/api/class.nedconverter_cpp.md#eulerENUToRotation_vec3_quat)*
- *[**eulerNEDToRotation**( const vec3 & )](../api/library/plugins/ig/api/class.nedconverter_cpp.md#eulerNEDToRotation_vec3_quat)*
- *[**eulerTARGETToRotation**( const vec3 & )](../api/library/plugins/ig/api/class.nedconverter_cpp.md#eulerTARGETToRotation_vec3_quat)*
- *[**rotationToEulerENU**( const quat & )](../api/library/plugins/ig/api/class.nedconverter_cpp.md#rotationToEulerENU_quat_vec3)*
- *[**rotationToEulerNED**( const quat & )](../api/library/plugins/ig/api/class.nedconverter_cpp.md#rotationToEulerNED_quat_vec3)*
- *[**rotationToEulerTARGET**( const quat & )](../api/library/plugins/ig/api/class.nedconverter_cpp.md#rotationToEulerTARGET_quat_vec3)*


## IG::IGConfig Class


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***getCloudTypes**( )* | Removed. |
| ***getPrecipitationTypes**( )* | Removed. |
| ***getLightning**( )* | Removed. |


## IG::INetworkManager Class


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| ***registrateClass**( int, CallbackBase * )* | Renamed. Use ***registerClass**( int, CallbackBase * )* instead. |


#### New Functions


- ***unregisterClass**( int )*
