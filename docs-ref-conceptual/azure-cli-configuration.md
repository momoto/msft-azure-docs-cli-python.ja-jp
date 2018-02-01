---
title: "Azure CLI 構成オプション"
description: "Azure CLI 2.0 を構成する方法"
keywords: "Azure CLI, 構成, 設定, Azure"
author: sptramer
ms.author: sttramer
manager: routlaw
ms.date: 12/13/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: azurecli
ms.service: multiple
ms.openlocfilehash: d60ede5b971ee2489482fb5a72bde9bf5389d37c
ms.sourcegitcommit: 8606f36963e8daa6448d637393d1e4ef2c9859a0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2018
---
# <a name="azure-cli-20-configuration"></a><span data-ttu-id="46ea9-104">Azure CLI 2.0 の構成</span><span class="sxs-lookup"><span data-stu-id="46ea9-104">Azure CLI 2.0 configuration</span></span>

<span data-ttu-id="46ea9-105">Azure CLI 2.0 を使用すると、ユーザー構成によってログ記録、データ収集などの内部設定を上書きして、一部の必須パラメーターに対して既定のオプションを指定できます。</span><span class="sxs-lookup"><span data-stu-id="46ea9-105">The Azure CLI 2.0 allows for user configuration to override internal settings such as logging and data collection, and provide default options for some required parameters.</span></span> <span data-ttu-id="46ea9-106">CLI は、こういった値のいくつかを管理するための便利なコマンド `az configure` を提供します。他の値については、構成ファイルまたは環境変数で設定できます。</span><span class="sxs-lookup"><span data-stu-id="46ea9-106">The CLI offers a convenience command for managing some of these values, `az configure`, and other values can be set in a configuration file or with environment variables.</span></span>

<span data-ttu-id="46ea9-107">CLI が使用する構成値は、次の優先順位で上から順番に評価されます。</span><span class="sxs-lookup"><span data-stu-id="46ea9-107">Configuration values used by the CLI are evaluted in the following precedence, with items higher on the list taking priority.</span></span>

1. <span data-ttu-id="46ea9-108">コマンドライン パラメーター</span><span class="sxs-lookup"><span data-stu-id="46ea9-108">Command-line parameters</span></span>
2. <span data-ttu-id="46ea9-109">環境変数</span><span class="sxs-lookup"><span data-stu-id="46ea9-109">Environment variables</span></span>
3. <span data-ttu-id="46ea9-110">構成ファイルの値または `az configure` で設定された値</span><span class="sxs-lookup"><span data-stu-id="46ea9-110">Values in the configuration file or set with `az configure`</span></span>

## <a name="cli-configuration-with-az-configure"></a><span data-ttu-id="46ea9-111">az configure での CLI 構成</span><span class="sxs-lookup"><span data-stu-id="46ea9-111">CLI configuration with az configure</span></span>

<span data-ttu-id="46ea9-112">CLI の既定値を [az configure](/cli/azure/?view=azure-cli-latest#az_configure) コマンドで設定します。</span><span class="sxs-lookup"><span data-stu-id="46ea9-112">You set defaults for the CLI with the [az configure](/cli/azure/?view=azure-cli-latest#az_configure) command.</span></span>
<span data-ttu-id="46ea9-113">このコマンドは 1 つの引数 `--defaults` を取ります。この引数は、スペースで区切られた `key=value` ペアのリストです。</span><span class="sxs-lookup"><span data-stu-id="46ea9-113">This command takes one argument, `--defaults`, which is a space-separated list of `key=value` pairs.</span></span> <span data-ttu-id="46ea9-114">指定した値は、必須の引数の代わりに、CLI によって使用されます。</span><span class="sxs-lookup"><span data-stu-id="46ea9-114">The provded values are used by the CLI in place of required arguments.</span></span>

<span data-ttu-id="46ea9-115">使用できるキーの一覧を次に示します。</span><span class="sxs-lookup"><span data-stu-id="46ea9-115">The following is a list of available keys that you can use.</span></span>

| <span data-ttu-id="46ea9-116">Name</span><span class="sxs-lookup"><span data-stu-id="46ea9-116">Name</span></span> | <span data-ttu-id="46ea9-117">[説明]</span><span class="sxs-lookup"><span data-stu-id="46ea9-117">Description</span></span> |
|------|-------------|
| <span data-ttu-id="46ea9-118">group</span><span class="sxs-lookup"><span data-stu-id="46ea9-118">group</span></span> | <span data-ttu-id="46ea9-119">すべてのコマンドに使用する既定のリソース グループ。</span><span class="sxs-lookup"><span data-stu-id="46ea9-119">The default resource group to use for all commands.</span></span> |
| <span data-ttu-id="46ea9-120">location</span><span class="sxs-lookup"><span data-stu-id="46ea9-120">location</span></span> | <span data-ttu-id="46ea9-121">すべてのコマンドに使用する既定の場所。</span><span class="sxs-lookup"><span data-stu-id="46ea9-121">The default location to use for all commands.</span></span> |
| <span data-ttu-id="46ea9-122">web</span><span class="sxs-lookup"><span data-stu-id="46ea9-122">web</span></span> | <span data-ttu-id="46ea9-123">`az webapp` コマンドに使用する既定のアプリ名。</span><span class="sxs-lookup"><span data-stu-id="46ea9-123">The default app name to use for `az webapp` commands.</span></span> |
| <span data-ttu-id="46ea9-124">vm</span><span class="sxs-lookup"><span data-stu-id="46ea9-124">vm</span></span> | <span data-ttu-id="46ea9-125">`az vm` コマンドに使用する既定の VM 名。</span><span class="sxs-lookup"><span data-stu-id="46ea9-125">The default VM name to use for `az vm` commands.</span></span> |
| <span data-ttu-id="46ea9-126">vmss</span><span class="sxs-lookup"><span data-stu-id="46ea9-126">vmss</span></span> | <span data-ttu-id="46ea9-127">`az vmss` コマンドに使用する既定の VMSS 名。</span><span class="sxs-lookup"><span data-stu-id="46ea9-127">The default VMSS name to use for  `az vmss` commands.</span></span> |
| <span data-ttu-id="46ea9-128">acr</span><span class="sxs-lookup"><span data-stu-id="46ea9-128">acr</span></span> | <span data-ttu-id="46ea9-129">`az acr` コマンドに使用する既定のコンテナー レジストリ名。</span><span class="sxs-lookup"><span data-stu-id="46ea9-129">The default container registry name to use for `az acr` commands.</span></span> |
| <span data-ttu-id="46ea9-130">acs</span><span class="sxs-lookup"><span data-stu-id="46ea9-130">acs</span></span> | <span data-ttu-id="46ea9-131">`az acs` コマンドに使用する既定のコンテナー サービス名。</span><span class="sxs-lookup"><span data-stu-id="46ea9-131">The default container service name to use for `az acs` commands.</span></span> |

<span data-ttu-id="46ea9-132">例として、すべてのコマンドの既定のリソース グループと場所を設定する方法を次に示します。</span><span class="sxs-lookup"><span data-stu-id="46ea9-132">As an example, here's how you would set the default resource group and location for all commands.</span></span>

```azurecli
az configure --defaults "location=westus2 group=MyResourceGroup"
```

## <a name="cli-configuration-file"></a><span data-ttu-id="46ea9-133">CLI 構成ファイル</span><span class="sxs-lookup"><span data-stu-id="46ea9-133">CLI configuration file</span></span>

<span data-ttu-id="46ea9-134">CLI 構成ファイルには、CLI の動作の管理に使用されるその他の設定が含まれています。</span><span class="sxs-lookup"><span data-stu-id="46ea9-134">The CLI configuration file contains other settings that are used for managing CLI behavior.</span></span> <span data-ttu-id="46ea9-135">構成ファイル自体は `$AZURE_CONFIG_DIR/config` にあります。</span><span class="sxs-lookup"><span data-stu-id="46ea9-135">The configuration file itself is located at `$AZURE_CONFIG_DIR/config`.</span></span> <span data-ttu-id="46ea9-136">`AZURE_CONFIG_DIR` の既定値は、Linux と macOS の場合は `$HOME/.azure/config`、Windows の場合は `%USERPROFILE%\.azure\config` です。</span><span class="sxs-lookup"><span data-stu-id="46ea9-136">The default value of `AZURE_CONFIG_DIR` is `$HOME/.azure/config` on Linux and macOS, and `%USERPROFILE%\.azure\config` on Windows.</span></span>

<span data-ttu-id="46ea9-137">構成ファイルは、INI ファイル形式で記述されます。</span><span class="sxs-lookup"><span data-stu-id="46ea9-137">Configuration files are written in the INI file format.</span></span> <span data-ttu-id="46ea9-138">こうしたファイルは、`[section-name]` ヘッダーで始まり、その後に `key=value` エントリのリストが続くセクションで構成されます。</span><span class="sxs-lookup"><span data-stu-id="46ea9-138">These files are made up of sections which start with a `[section-name]` header, followed by a list of `key=value` entries.</span></span> <span data-ttu-id="46ea9-139">セクション名は大文字と小文字が区別され、キー名は区別されません。</span><span class="sxs-lookup"><span data-stu-id="46ea9-139">Section names are case-sensitive and key names are not.</span></span>
<span data-ttu-id="46ea9-140">`#` または `;` で始まる行はすべてコメントです。</span><span class="sxs-lookup"><span data-stu-id="46ea9-140">Comments are any line that begins with a `#` or `;`.</span></span> <span data-ttu-id="46ea9-141">インライン コメントは許可されていません。</span><span class="sxs-lookup"><span data-stu-id="46ea9-141">Inline comments are not allowed.</span></span> <span data-ttu-id="46ea9-142">ブール値は、大文字と小文字が区別されず、次の値によって表されます。</span><span class="sxs-lookup"><span data-stu-id="46ea9-142">Booleans are case-insensitive, and are represented by the following values.</span></span>

* <span data-ttu-id="46ea9-143">__True__: 1、yes、true、on</span><span class="sxs-lookup"><span data-stu-id="46ea9-143">__True__: 1, yes, true, on</span></span>
* <span data-ttu-id="46ea9-144">__False__: 0、no、false、off</span><span class="sxs-lookup"><span data-stu-id="46ea9-144">__False__: 0, no, false, off</span></span>

<span data-ttu-id="46ea9-145">次の例は、確認のプロンプトを無効にして、`/var/log/azure` ディレクトリへのログ記録を設定する CLI 構成ファイルです。</span><span class="sxs-lookup"><span data-stu-id="46ea9-145">Here's an example of a CLI configuration file which disables any confirmation prompts and sets up logging to the `/var/log/azure` directory.</span></span>

```
[core]
disable_confirm_prompt=Yes

[logging]
enable_log_file=yes
log_dir=/var/log/azure
```

<span data-ttu-id="46ea9-146">使用できる構成値とその意味の詳細については、次のセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="46ea9-146">See the next section for details on all of the available configuration values and what they mean.</span></span> <span data-ttu-id="46ea9-147">INI ファイル形式の詳細については、[INI に関する Python のドキュメント](https://docs.python.org/3/library/configparser.html#supported-ini-file-structure)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="46ea9-147">For the full details on the INI file format, see the [Python documentation on INI](https://docs.python.org/3/library/configparser.html#supported-ini-file-structure).</span></span>

## <a name="cli-configuration-values-and-environment-variables"></a><span data-ttu-id="46ea9-148">CLI 構成値と環境変数</span><span class="sxs-lookup"><span data-stu-id="46ea9-148">CLI configuration values and environment variables</span></span>

<span data-ttu-id="46ea9-149">次の表は、構成ファイルで指定できるすべてのセクションとオプションの名前を示しています。</span><span class="sxs-lookup"><span data-stu-id="46ea9-149">The following table contains all of the sections and option names that can be placed in a configuration file.</span></span> <span data-ttu-id="46ea9-150">対応する環境変数は、`AZURE_{section}_{name}` としてすべて大文字で設定できます。</span><span class="sxs-lookup"><span data-stu-id="46ea9-150">Their corresponding environment variables can be set as `AZURE_{section}_{name}`, in all caps.</span></span> <span data-ttu-id="46ea9-151">たとえば、`batchai` セクションの `storage_account` の既定値は、`AZURE_BATCHAI_STORAGE_ACCOUNT` 変数で設定します。</span><span class="sxs-lookup"><span data-stu-id="46ea9-151">For example, you can set the `batchai` section's `storage_account` default in the `AZURE_BATCHAI_STORAGE_ACCOUNT` variable.</span></span>

<span data-ttu-id="46ea9-152">既定値を使用できる値は、必須の場合でも、コマンド ライン引数に存在する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="46ea9-152">Any value with a default available does not have to be present in the command line arguments, even if it is required.</span></span>

| <span data-ttu-id="46ea9-153">セクション</span><span class="sxs-lookup"><span data-stu-id="46ea9-153">Section</span></span> | <span data-ttu-id="46ea9-154">Name</span><span class="sxs-lookup"><span data-stu-id="46ea9-154">Name</span></span>      | <span data-ttu-id="46ea9-155">type</span><span class="sxs-lookup"><span data-stu-id="46ea9-155">Type</span></span> | <span data-ttu-id="46ea9-156">[説明]</span><span class="sxs-lookup"><span data-stu-id="46ea9-156">Description</span></span>|
|---------|-----------|------|------------|
| <span data-ttu-id="46ea9-157">__core__</span><span class="sxs-lookup"><span data-stu-id="46ea9-157">__core__</span></span> | <span data-ttu-id="46ea9-158">output</span><span class="sxs-lookup"><span data-stu-id="46ea9-158">output</span></span> | <span data-ttu-id="46ea9-159">文字列</span><span class="sxs-lookup"><span data-stu-id="46ea9-159">string</span></span> | <span data-ttu-id="46ea9-160">既定の出力形式。</span><span class="sxs-lookup"><span data-stu-id="46ea9-160">The default output format.</span></span> <span data-ttu-id="46ea9-161">`json`、`jsonc`、`tsv`、`table` のいずれかを指定できます。</span><span class="sxs-lookup"><span data-stu-id="46ea9-161">Can be one of `json`, `jsonc`, `tsv`, or `table`.</span></span> |
| | <span data-ttu-id="46ea9-162">disable\_confirm\_prompt</span><span class="sxs-lookup"><span data-stu-id="46ea9-162">disable\_confirm\_prompt</span></span> | <span data-ttu-id="46ea9-163">ブール値</span><span class="sxs-lookup"><span data-stu-id="46ea9-163">boolean</span></span> | <span data-ttu-id="46ea9-164">確認のプロンプトをオン/オフにします。</span><span class="sxs-lookup"><span data-stu-id="46ea9-164">Turn confirmation prompts on/off.</span></span> |
| | <span data-ttu-id="46ea9-165">collect\_telemetry</span><span class="sxs-lookup"><span data-stu-id="46ea9-165">collect\_telemetry</span></span> | <span data-ttu-id="46ea9-166">ブール値</span><span class="sxs-lookup"><span data-stu-id="46ea9-166">boolean</span></span> | <span data-ttu-id="46ea9-167">Microsoft による、CLI の使用に関する匿名データの収集を許可します。</span><span class="sxs-lookup"><span data-stu-id="46ea9-167">Allow Microsoft to collect anonymous data on the usage of the CLI.</span></span> <span data-ttu-id="46ea9-168">プライバシー情報については、[Azure CLI 2.0 の使用条件](http://aka.ms/AzureCliLegal)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="46ea9-168">For privacy information, see the [Azure CLI 2.0 Terms of Use](http://aka.ms/AzureCliLegal).</span></span> |
| <span data-ttu-id="46ea9-169">__logging__</span><span class="sxs-lookup"><span data-stu-id="46ea9-169">__logging__</span></span> | <span data-ttu-id="46ea9-170">enable\_log\_file</span><span class="sxs-lookup"><span data-stu-id="46ea9-170">enable\_log\_file</span></span> | <span data-ttu-id="46ea9-171">ブール値</span><span class="sxs-lookup"><span data-stu-id="46ea9-171">boolean</span></span> | <span data-ttu-id="46ea9-172">ログ記録をオン/オフにします。</span><span class="sxs-lookup"><span data-stu-id="46ea9-172">Turn logging on/off.</span></span> |
| | <span data-ttu-id="46ea9-173">log\_dir</span><span class="sxs-lookup"><span data-stu-id="46ea9-173">log\_dir</span></span> | <span data-ttu-id="46ea9-174">文字列</span><span class="sxs-lookup"><span data-stu-id="46ea9-174">string</span></span> | <span data-ttu-id="46ea9-175">ログを書き込むディレクトリ。</span><span class="sxs-lookup"><span data-stu-id="46ea9-175">The directory to write logs to.</span></span> <span data-ttu-id="46ea9-176">既定では `${AZURE_CONFIG_DIR}/logs` です。</span><span class="sxs-lookup"><span data-stu-id="46ea9-176">By default this is `${AZURE_CONFIG_DIR}/logs`.</span></span> |
| <span data-ttu-id="46ea9-177">__storage__</span><span class="sxs-lookup"><span data-stu-id="46ea9-177">__storage__</span></span> | <span data-ttu-id="46ea9-178">connection\_string</span><span class="sxs-lookup"><span data-stu-id="46ea9-178">connection\_string</span></span> | <span data-ttu-id="46ea9-179">文字列</span><span class="sxs-lookup"><span data-stu-id="46ea9-179">string</span></span> | <span data-ttu-id="46ea9-180">`az storage` コマンドに使用する既定の接続文字列。</span><span class="sxs-lookup"><span data-stu-id="46ea9-180">The default connection string to use for `az storage` commands.</span></span> |
| | <span data-ttu-id="46ea9-181">アカウント</span><span class="sxs-lookup"><span data-stu-id="46ea9-181">account</span></span> | <span data-ttu-id="46ea9-182">文字列</span><span class="sxs-lookup"><span data-stu-id="46ea9-182">string</span></span> | <span data-ttu-id="46ea9-183">`az storage` コマンドに使用する既定のアカウント名。</span><span class="sxs-lookup"><span data-stu-id="46ea9-183">The default account name to use for `az storage` commands.</span></span> |
| | <span data-ttu-id="46ea9-184">key</span><span class="sxs-lookup"><span data-stu-id="46ea9-184">key</span></span> | <span data-ttu-id="46ea9-185">文字列</span><span class="sxs-lookup"><span data-stu-id="46ea9-185">string</span></span> | <span data-ttu-id="46ea9-186">`az storage` コマンドに使用する既定のアカウント キー。</span><span class="sxs-lookup"><span data-stu-id="46ea9-186">The default account key to use for `az storage` commands.</span></span> |
| | <span data-ttu-id="46ea9-187">sas\_token</span><span class="sxs-lookup"><span data-stu-id="46ea9-187">sas\_token</span></span> | <span data-ttu-id="46ea9-188">文字列</span><span class="sxs-lookup"><span data-stu-id="46ea9-188">string</span></span> | <span data-ttu-id="46ea9-189">`az storage` コマンドに使用する既定の SAS トークン。</span><span class="sxs-lookup"><span data-stu-id="46ea9-189">The default SAS token to use for `az storage` commands.</span></span> |
| <span data-ttu-id="46ea9-190">__batchai__</span><span class="sxs-lookup"><span data-stu-id="46ea9-190">__batchai__</span></span> | <span data-ttu-id="46ea9-191">storage\_account</span><span class="sxs-lookup"><span data-stu-id="46ea9-191">storage\_account</span></span> | <span data-ttu-id="46ea9-192">文字列</span><span class="sxs-lookup"><span data-stu-id="46ea9-192">string</span></span> | <span data-ttu-id="46ea9-193">`az batchai` コマンドに使用する既定のストレージ アカウント。</span><span class="sxs-lookup"><span data-stu-id="46ea9-193">The default storage account to use for `az batchai` commands.</span></span> |
| | <span data-ttu-id="46ea9-194">storage\_key</span><span class="sxs-lookup"><span data-stu-id="46ea9-194">storage\_key</span></span> | <span data-ttu-id="46ea9-195">文字列</span><span class="sxs-lookup"><span data-stu-id="46ea9-195">string</span></span> | <span data-ttu-id="46ea9-196">`az batchai` コマンドに使用する既定のストレージ キー。</span><span class="sxs-lookup"><span data-stu-id="46ea9-196">The default storage key to use for `az batchai` commands.</span></span> |
| <span data-ttu-id="46ea9-197">__batch__</span><span class="sxs-lookup"><span data-stu-id="46ea9-197">__batch__</span></span> | <span data-ttu-id="46ea9-198">アカウント</span><span class="sxs-lookup"><span data-stu-id="46ea9-198">account</span></span> | <span data-ttu-id="46ea9-199">文字列</span><span class="sxs-lookup"><span data-stu-id="46ea9-199">string</span></span> | <span data-ttu-id="46ea9-200">`az batch` コマンドに使用する既定の Azure Batch アカウント名。</span><span class="sxs-lookup"><span data-stu-id="46ea9-200">The default Azure Batch account name to use for `az batch` commands.</span></span> |
| | <span data-ttu-id="46ea9-201">access\_key</span><span class="sxs-lookup"><span data-stu-id="46ea9-201">access\_key</span></span> | <span data-ttu-id="46ea9-202">文字列</span><span class="sxs-lookup"><span data-stu-id="46ea9-202">string</span></span> | <span data-ttu-id="46ea9-203">`az batch` コマンドに使用する既定のアクセス キー。</span><span class="sxs-lookup"><span data-stu-id="46ea9-203">The default access key to use for `az batch` commands.</span></span> <span data-ttu-id="46ea9-204">`aad` 承認でのみ使用されます。</span><span class="sxs-lookup"><span data-stu-id="46ea9-204">Only used with `aad` authorization.</span></span> |
| | <span data-ttu-id="46ea9-205">endpoint</span><span class="sxs-lookup"><span data-stu-id="46ea9-205">endpoint</span></span> | <span data-ttu-id="46ea9-206">文字列</span><span class="sxs-lookup"><span data-stu-id="46ea9-206">string</span></span> | <span data-ttu-id="46ea9-207">`az batch` コマンドに対する既定の接続先エンドポイント。</span><span class="sxs-lookup"><span data-stu-id="46ea9-207">The default endpoint to connect to for `az batch` commands.</span></span> |
| | <span data-ttu-id="46ea9-208">auth\_mode</span><span class="sxs-lookup"><span data-stu-id="46ea9-208">auth\_mode</span></span> | <span data-ttu-id="46ea9-209">文字列</span><span class="sxs-lookup"><span data-stu-id="46ea9-209">string</span></span> | <span data-ttu-id="46ea9-210">`az batch` コマンドに使用する承認モード。</span><span class="sxs-lookup"><span data-stu-id="46ea9-210">The authorization mode to use for `az batch` commands.</span></span> <span data-ttu-id="46ea9-211">`shared_key` または `aad` を指定できます。</span><span class="sxs-lookup"><span data-stu-id="46ea9-211">Can be `shared_key` or `aad`.</span></span> |

> [!NOTE]
> <span data-ttu-id="46ea9-212">構成ファイルに他の値が含まれる場合もありますが、その値は、`az configure` などの CLI コマンドで直接管理されます。</span><span class="sxs-lookup"><span data-stu-id="46ea9-212">You may see other values in your configuration file, but these are managed directly through CLI commands, including `az configure`.</span></span> <span data-ttu-id="46ea9-213">上記の表は、自身で変更する必要がある値のみを示しています。</span><span class="sxs-lookup"><span data-stu-id="46ea9-213">The ones listed in the table above are the only values you should change yourself.</span></span>